# 17 — Security Audit & Vulnerability Assessment

## 1. Security Architecture Review

Tourvaa exhibits robust defense-in-depth security engineering:
1. **Dual Cryptographic Domains**: Separate secret keys prevent external portal users from forging admin JWT tokens.
2. **HttpOnly Session Cookies**: Eliminates credential theft via client-side cross-site scripting (XSS).
3. **Database Secrets Encryption**: API keys and payment secrets are encrypted using AES-256-GCM at rest.
4. **Webhook Signature Verification**: Both Stripe (HMAC-SHA256) and PayPal transmission headers are strictly validated with 300-second replay rejection windows.
5. **Private Document Storage**: Sensitive documents (invoices, receipts, partner KYC IDs) are stored in `private-docs/` outside the public `/storage` mount, accessible only via authenticated endpoints that verify entity ownership.
6. **SQL Injection Prevention**: All database queries utilize SQLAlchemy parameterized queries and ORM objects. Raw string interpolations are prohibited.
7. **Cross-Site Scripting (XSS)**: Rich text descriptions in CMS blogs are sanitized using Bleach before storage.
8. **Brute Force Lockout**: Accounts lock automatically for 15 minutes after 5 consecutive failed login attempts.

---

## 2. Security Findings & Recommendations

| ID | Severity | Module | Finding | Source Evidence | Impact | Remediation Recommendation |
|---|---|---|---|---|---|---|
| **SEC-01** | **Low** | Settings / Storage | Local storage used as fallback when Cloudinary is unconfigured. | [`app/routers/uploads.py`](../tourvaa-admin-backend/app/routers/uploads.py) | In multi-instance deployments, local uploads will not replicate across container replicas. | Ensure Cloudinary is mandatory in production deployments. |
| **SEC-02** | **Informational**| GeoIP | Free tier `ip-api.com` is default provider. | [`app/config/__init__.py`](../tourvaa-admin-backend/app/config/__init__.py) | Free tier of ip-api is not licensed for commercial production traffic. | Switch `GEOIP_PROVIDER` to `ipapi` with a licensed commercial API key. |
