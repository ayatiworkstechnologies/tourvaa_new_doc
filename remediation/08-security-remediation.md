# Chapter 08 — Security Remediation

## 1. Overview of Security Vulnerabilities Resolved

Security remediation focused on hardening cross-site request forgery protections, maintaining strict role-based access control (RBAC) boundaries, and ensuring clean session termination.

---

## 2. BUG-001: CSRF Protection Hardening

### Threat Model & Attack Vector
- **Vulnerability**: Incomplete Double-Submit Cookie CSRF Validation.
- **Mechanism**:
  An attacker constructs a malicious webpage that executes a background `POST` request to `https://api.tourvaa.com/api/bookings/1/cancel`.
  Because the browser automatically attaches existing session cookies (`tourvaa_access`), the endpoint would execute using the victim's authenticated session.
  In the pre-remediation code, the CSRF check only triggered if the `tourvaa_csrf` cookie was sent. If the attacker suppressed or failed to provide that cookie, the middleware evaluated `if cookie_token:` as `False` and passed the request to the endpoint handler!
- **Remediation**:
  The middleware was updated to inspect whether any browser session authentication cookie is present:
  ```python
  auth_cookie = (
      request.cookies.get(access_cookie_name(portal))
      or request.cookies.get("tourvaa_access")
      or request.cookies.get("tourvaa_admin_access")
  )
  cookie_token = request.cookies.get(csrf_cookie_name(portal))
  if auth_cookie or cookie_token:
      header_token = request.headers.get(CSRF_HEADER_NAME)
      if not cookie_token or not header_token or header_token != cookie_token:
          return JSONResponse(status_code=403, content={"status": "error", "message": "CSRF token missing or invalid"})
  ```
- **Verification**:
  - `test_csrf_blocks_cookie_auth_without_csrf_header` -> HTTP 403 Forbidden (Attack blocked).
  - `test_csrf_allows_matching_double_submit_cookies` -> HTTP 200 OK (Legitimate browser request allowed).
  - `test_csrf_allows_bearer_token_requests` -> HTTP 200 OK (Mobile & API clients preserved).

---

## 3. BUG-010: Role-Based Navigation Boundary Consistency

### Threat & Usability Gap
The RBAC specification designates `sub-admin` as an administrative back-office role. Omitting `sub-admin` from `PublicHeader.tsx` allowed back-office operators to see customer-facing shopping controls when browsing the storefront, violating role separation.

### Remediation
Updated `src/components/public/PublicHeader.tsx` line 71:
```typescript
const isAdminRole = ["admin", "super-admin", "sub-admin"].includes(roleSlug.toLowerCase());
```
This guarantees consistent role-based UI separation across all staff tiers.

---

## 4. BUG-005: Clean Token Revocation on Multi-Role Logout

### Threat & Reliability Gap
When logging out from a multi-role portal after a role mismatch, overly complex header requirements risked leaving valid session cookies in the browser, enabling session confusion on subsequent logins.

### Remediation
Standardized `PortalAuthPage.tsx` to issue `await api.post("/auth/logout").catch(() => {});`, ensuring that the backend logout handler invalidates and flushes session cookies cleanly.
