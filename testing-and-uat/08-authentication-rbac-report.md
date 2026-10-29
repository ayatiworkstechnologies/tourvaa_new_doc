# 08 — Authentication, Session & Role-Based Access Control Report
**Tourvaa Travel & Tourism Experience Platform**

---

### 1. Authentication Architecture & Security Baseline

Authentication in the Tourvaa platform utilizes a dual-layer strategy:
1. **JSON Web Tokens (JWT)**: Signed with secret keys using the `HS256` HMAC algorithm. Tokens encode `sub` (user ID), `email`, `role`, and `token_version`.
2. **HttpOnly Secure Session Cookies**: Delivered via `Set-Cookie` with `HttpOnly`, `SameSite=Lax`, and `Secure` attributes (`tourvaa_access`), preventing XSS token theft.

```
Authentication Security Controls:
├── Token Expiration:            1,440 minutes (24 hours) for standard sessions
├── Invalidation Mechanism:      token_version increment in database revokes all active JWTs
├── Brute-Force Rate Limiting:   10 requests / 60 seconds per IP on /auth/login
├── Consecutive Failure Lockout: 5 failed attempts -> 15-minute account lock (HTTP 423)
├── Two-Factor Auth (MFA):       Time-based One-Time Password (TOTP) + 8 backup codes
└── Password Encryption:         Bcrypt with salt rounds >= 12
```

---

### 2. User Roles & Portal Scopes

The system architecture defines **9 discrete user roles** verified in the database `roles` table:

| Role ID | Role Name | Slug | System Role | Authorized Portal Boundary | Primary Operational Responsibilities |
| :---: | :--- | :--- | :---: | :--- | :--- |
| **1** | Super Admin | `super-admin` | Yes | `/admin/*` | Global platform administration, database settings, audit logs, and security oversight. |
| **2** | Admin | `admin` | Yes | `/admin/*` | Agency approvals, tour review and publishing, financial reports, and user moderation. |
| **3** | Sub Admin | `sub-admin` | Yes | `/admin/*` | Content management, customer verification, and itinerary curation. |
| **4** | Supplier | `supplier` | Yes | `/supplier/*` | Tour package creation, inventory allotment management, and supplier invoice tracking. |
| **5** | Agent / Reseller | `agent-reseller` | Yes | `/agent/*` | B2B catalog exploration, booking creation for clients, commission ledgers, and payouts. |
| **6** | Customer | `customer` | Yes | `/customer/*` | Tour booking, wishlist management, review submission, and support ticket management. |
| **7** | Affiliate | `affiliate` | Yes | `/affiliate/*` | Server-tracked short link generation, referral click tracking, and commission payouts. |
| **8** | Accountant | `accountant` | No | `/admin/finance` | Financial ledger auditing, supplier disbursements, and tax reporting. |
| **9** | Demo | `demo` | No | Restricted | Read-only evaluation workspace for sales and walkthrough demonstrations. |

---

### 3. Role-Based Access Control (RBAC) Testing Matrix

The following test matrix summarizes empirical verification of authorization boundaries across primary modules:

| Role | Target Endpoint / Route | Action Attempted | Expected Status | Actual Status | RBAC Verdict |
| :--- | :--- | :--- | :---: | :---: | :---: |
| **Unauthenticated** | `GET /api/users/me` | Fetch profile without token | 401 Unauthorized | 401 Unauthorized | **PASSED** |
| **Unauthenticated** | `GET /api/admin/dashboard` | Access admin dashboard | 401 Unauthorized | 401 Unauthorized | **PASSED** |
| **Customer** | `GET /api/admin/settings` | Access platform settings | 403 Forbidden | 403 Forbidden | **PASSED** |
| **Customer** | `POST /api/tours` | Attempt tour creation | 403 Forbidden | 403 Forbidden | **PASSED** |
| **Customer** | `GET /api/customers/me/bookings` | View own booking history | 200 OK | 200 OK | **PASSED** |
| **Customer** | `GET /api/bookings/{other_id}` | Attempt viewing other's booking | 403 Forbidden | 403 Forbidden | **PASSED** |
| **Supplier** | `POST /api/tours` | Create tour for approval | 201 Created | 201 Created | **PASSED** |
| **Supplier** | `PUT /api/tours/{id}/publish` | Attempt immediate publication | 403 Forbidden | 403 Forbidden | **PASSED** |
| **Supplier** | `GET /api/supplier/bookings` | View bookings for own tours | 200 OK | 200 OK | **PASSED** |
| **Agent** | `POST /api/bookings` | Create client booking | 201 Created | 201 Created | **PASSED** |
| **Agent** | `GET /api/agent/commissions` | View earned commission ledger | 200 OK | 200 OK | **PASSED** |
| **Affiliate** | `GET /api/affiliate/clicks` | View referral click logs | 200 OK | 200 OK | **PASSED** |
| **Affiliate** | `POST /api/tours` | Attempt tour creation | 403 Forbidden | 403 Forbidden | **PASSED** |
| **Admin** | `PUT /api/tours/{id}/publish` | Approve and publish tour | 200 OK | 200 OK | **PASSED** |
| **Admin** | `GET /api/admin/audit-logs` | Review platform audit trail | 200 OK | 200 OK | **PASSED** |

---

### 4. Brute-Force & Session Security Verification

1. **Consecutive Bad Passwords Lockout**:
   - Tested via `test_02_auth.py::test_login_repeated_bad_passwords_lock_the_account`.
   - Repeated failed login attempts against a test account correctly incremented `failed_login_attempts`.
   - On the 5th failed attempt, the account was locked with a timestamp set in `locked_until`, returning `HTTP 423 Locked`. Subsequent attempts with the valid password were appropriately blocked until the lockout duration expired.
2. **Session Invalidation (Token Version)**:
   - When a user changes their password or triggers administrative deactivation, `token_version` is incremented.
   - Any previously issued JWT containing the stale `token_version` is immediately rejected by the `get_current_user` dependency, preventing session hijacking.
