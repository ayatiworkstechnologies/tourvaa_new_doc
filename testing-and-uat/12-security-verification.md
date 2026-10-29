# 12 — Security Verification & Vulnerability Assessment
**Tourvaa Travel & Tourism Experience Platform**

---

### 1. Security Architecture & Threat Model

The Tourvaa platform security posture was audited against the **OWASP Top 10 (2021)** enterprise web application vulnerability categories using non-invasive static source audits, cryptographic inspection, and HTTP boundary probes.

```
Security Control Architecture:
├── Transport Encryption:      Enforced HTTPS / TLS 1.3 across production ingress
├── Authentication Tokens:     HMAC-SHA256 signed JWTs with 24-hour expiration
├── Session Cookie Flags:      HttpOnly, Secure, SameSite=Lax (Cookie: tourvaa_access)
├── Password Security:         Bcrypt salted hash with >= 12 rounds
├── Brute-Force Defense:       10 req/min rate limit; 5 bad passwords -> 15 min lock
└── Access Control:            RBAC middleware with 318 granular permissions
```

---

### 2. OWASP Top 10 Security Audit Findings

| OWASP Category | Vulnerability Surface | Observed Implementation | Risk Level | Audit Finding |
| :--- | :--- | :--- | :---: | :--- |
| **A01: Broken Access Control** | Route endpoints & user data | Strict `require_role()` dependency checks on administrative endpoints. | Low | **COMPLIANT** |
| **A02: Cryptographic Failures**| Data in transit & rest | Passwords hashed with Bcrypt. Secrets isolated in `.env` and masked. | Low | **COMPLIANT** |
| **A03: Injection** | SQL queries & forms | SQLAlchemy ORM parameterized queries; AST scan confirms 0 raw string interpolations. | Low | **COMPLIANT** |
| **A04: Insecure Design** | Rate limiting & lockout | IP rate limiting on login; consecutive failure lockout enforced in DB (`locked_until`). | Low | **COMPLIANT** |
| **A05: Security Misconfig** | CSRF Protection Middleware | [`app/middleware/csrf.py:101-105`](../../tourvaa-admin-backend/app/middleware/csrf.py#L101-L105) allows mutating requests with missing `Origin`/`Referer`. | **CRITICAL** | **CONFIRMED DEFECT (P0)** |
| **A06: Vulnerable Dependencies**| Python & Node packages | Modern baseline (FastAPI 0.115, Next.js 14.2.35). | Low | **COMPLIANT** |
| **A07: Identification & Auth** | Sessions & 2FA | Multi-factor TOTP provisioning with backup codes; `token_version` invalidation. | Low | **COMPLIANT** |
| **A08: Software & Data Integrity**| Database session lifecycle | [`app/database/__init__.py:35-43`](../../tourvaa-admin-backend/app/database/__init__.py#L35-L43) `get_db` omits explicit `db.rollback()` on unhandled exceptions. | **CRITICAL** | **CONFIRMED DEFECT (P0)** |
| **A09: Logging & Monitoring** | Audit trail | Administrative actions logged to `audit_logs` table (2,588 entries recorded). | Low | **COMPLIANT** |
| **A10: SSRF** | Third-party webhooks | Outbound integrations restricted to whitelisted payment and tour provider endpoints. | Low | **COMPLIANT** |

---

### 3. Detailed Audit of Confirmed Security Defects

#### 3.1 P0 Defect: CSRF Middleware Header Bypass ([csrf.py:101-105](../../tourvaa-admin-backend/app/middleware/csrf.py#L101-L105))
- **Source Evidence**:
  ```python
  origin = request.headers.get("origin")
  referer = request.headers.get("referer")
  if not origin and not referer:
      # If neither header is present, allow the request through
      return await call_next(request)
  ```
- **Vulnerability Mechanism**: While browser requests typically include `Origin` or `Referer`, certain older browsers or privacy extensions strip these headers. An attacker can craft a Cross-Site Request Forgery exploit that suppresses these headers, bypassing CSRF validation entirely on state-changing `POST`, `PUT`, or `DELETE` requests.
- **Remediation**: Mutating browser requests must strictly require a valid Origin or Referer header matching `settings.ALLOWED_ORIGINS`:
  ```python
  if request.method in ("POST", "PUT", "PATCH", "DELETE"):
      if not origin and not referer:
          return JSONResponse(status_code=403, content={"detail": "CSRF origin header required"})
  ```

#### 3.2 P0 Defect: Database Session Leak on Exception ([session.py:35-43](../../tourvaa-admin-backend/app/database/__init__.py#L35-L43))
- **Source Evidence**:
  ```python
  def get_db():
      db = SessionLocal()
      try:
          yield db
      finally:
          db.close()
  ```
- **Vulnerability Mechanism**: In the event of an unhandled exception during database write operations, the session is closed without calling `db.rollback()`. In SQLAlchemy connection pooling, returning a dirty connection to the pool causes subsequent requests using that pooled connection to execute inside an uncommitted transaction state.
- **Remediation**: Wrap session lifecycle in an explicit `except Exception:` block with `db.rollback()`.
