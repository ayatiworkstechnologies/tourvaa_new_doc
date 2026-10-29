# 09 — Authentication, Authorization & Security Architecture

## 1. Dual-Domain JWT Authentication

To defend against privilege escalation, Tourvaa segregates user sessions into two independent cryptographic domains:
1. **`admin` Domain**: Used exclusively by back-office roles (`super-admin`, `admin`, `sub-admin`). Tokens are signed using `ADMIN_JWT_SECRET_KEY`.
2. **`normal` Domain**: Used by external marketplace users (`customer`, `supplier`, `agent-reseller`, `affiliate`). Tokens are signed using `NORMAL_JWT_SECRET_KEY`.

At startup, the system validates that `ADMIN_JWT_SECRET_KEY != NORMAL_JWT_SECRET_KEY`. Even if a compromised portal user modifies their role claim, the token cannot decode against the admin secret key.

---

## 2. Session Cookies & Token Storage

Authentication operates primarily via **`httpOnly`, `Secure`, `SameSite=Lax` cookies**:
- `tourvaa_access`: Short-lived access JWT (24-hour expiration).
- `tourvaa_refresh`: Long-lived refresh JWT (30-day expiration).

Browser JavaScript cannot read or exfiltrate these cookies via XSS. When programmatic clients connect, standard `Authorization: Bearer <token>` headers are accepted as fallbacks.

---

## 3. Account Lockout & Brute-Force Defenses

- **Threshold**: 5 consecutive invalid password attempts.
- **Lockout Duration**: 15 minutes (`locked_until`).
- **Reset**: A successful login immediately clears `failed_login_attempts`.
- **Global Invalidation (`token_version`)**: Incrementing `user.token_version` on password reset or remote logout instantly revokes all active JWTs.

---

## 4. Role-Based Access Control (RBAC) Matrix

Permissions follow a dual naming convention supported by `expand_permission_slugs`:
- Dotted format: `module.action` (e.g. `tours.view`, `bookings.edit`)
- Hyphenated format: `action-module` (e.g. `view-tours`, `update-bookings`)

| Permission Slug | Super Admin | Admin | Sub Admin | Supplier | Agent | Customer | Affiliate |
|---|---|---|---|---|---|---|---|
| `tours.view` | Yes | Yes | Yes | Own Tours | Yes | Yes | Yes |
| `tours.create` / `edit` | Yes | Yes | With Perm | Own Tours | No | No | No |
| `tours.approve` | Yes | Yes | No | No | No | No | No |
| `bookings.view` | Yes | Yes | Yes | Own Bookings | Own Clients | Own Bookings | No |
| `bookings.edit` | Yes | Yes | With Perm | Status Dec. | No | No | No |
| `payments.view` | Yes | Yes | Yes | No | Own Billed | Own Paid | No |
| `payments.refund` | Yes | Yes | No | No | No | No | No |
| `supplier_ledger.view`| Yes | Yes | No | Own Ledger | No | No | No |
| `agent_ledger.view` | Yes | Yes | No | No | Own Ledger | No | No |
| `affiliate_payouts.view`| Yes | Yes | No | No | No | No | Own Wallet |
| `settings.edit` | Yes | No | No | No | No | No | No |
