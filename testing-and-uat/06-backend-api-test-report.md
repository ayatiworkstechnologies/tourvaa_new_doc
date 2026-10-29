# 06 — Backend API Testing Matrix & Endpoint Assessment
**Tourvaa Travel & Tourism Experience Platform**

---

### 1. API Architecture & Inventory Baseline

The backend API engine is developed using **FastAPI 0.115.0** and **Pydantic v2**. 

```
Backend API Scale:
├── Total API Paths:         594 distinct route paths
├── Total HTTP Operations:   785 operations
├── Router Tag Groups:       61 OpenAPI router tags
├── Base Endpoint URL:       http://127.0.0.1:8000/api
└── Pytest Automation:       110 test files with 864 test functions in tests/
```

---

### 2. Router Group Testing Matrix

The following matrix documents the verification results across the primary API router domains:

| Router Domain | Route Prefix | Total Ops | Auth Required | Request Validation | Status Codes Tested | Test Suite Reference | Result |
| :--- | :--- | :---: | :---: | :---: | :--- | :--- | :---: |
| **Authentication** | `/auth` | 18 | Public / Bearer | Pydantic v2 | 200, 400, 401, 422, 429 | `test_02_auth.py` | **PASSED** |
| **Users & Roles** | `/users`, `/roles` | 24 | Bearer (Admin) | Pydantic v2 | 200, 201, 403, 404, 422 | `test_03_rbac.py` | **PASSED** |
| **Agencies & Branches** | `/agencies`, `/branches` | 26 | Bearer | Pydantic v2 | 200, 201, 403, 404 | `test_08_agents.py` | **PASSED** |
| **Tours & Itineraries** | `/tours`, `/itineraries` | 52 | Mixed (Public/Admin) | Pydantic v2 | 200, 201, 404, 422 | `test_14_basic_tours.py` | **PASSED** |
| **Tour Packages & Pricing**| `/pricing`, `/packages` | 34 | Bearer | Pydantic v2 | 200, 201, 400, 404 | `test_15_advanced_tour_cms.py` | **PASSED** |
| **Bookings & Reservations**| `/bookings` | 46 | Bearer | Pydantic v2 | 200, 201, 400, 404, 409 | `test_booking_flow_unit.py` | **PASSED** |
| **Payments & Escrow** | `/payments`, `/crypto` | 38 | Bearer | Pydantic v2 | 200, 201, 400, 402, 502 | `test_booking_financials_unit.py`| **PASSED** |
| **Inventory & Allotments** | `/inventory`, `/allotments`| 22 | Bearer | Pydantic v2 | 200, 201, 409, 422 | `test_booking_flow_unit.py` | **PASSED** |
| **Customers & Leads** | `/customers`, `/leads` | 30 | Bearer | Pydantic v2 | 200, 201, 403, 404 | `test_06_customers.py` | **PASSED** |
| **Suppliers Management** | `/suppliers` | 28 | Bearer | Pydantic v2 | 200, 201, 403, 404 | `test_07_suppliers.py` | **PASSED** |
| **Agents & Resellers** | `/agents` | 24 | Bearer | Pydantic v2 | 200, 201, 403, 404 | `test_08_agents.py` | **PASSED** |
| **Affiliate Engine** | `/affiliates`, `/referrals`| 28 | Mixed (Public/Affiliate)| Pydantic v2 | 200, 201, 403, 404 | `test_41_affiliate_module_v2.py`| **PASSED** |
| **Messaging & Chat** | `/messages`, `/chat` | 26 | Bearer / WS | Pydantic v2 | 200, 201, 403, 404 | `test_messaging_serialization_unit.py`| **PASSED** |
| **Finance & Ledger** | `/finance`, `/commissions`| 32 | Bearer (Finance) | Pydantic v2 | 200, 201, 403, 404 | `test_booking_financials_unit.py`| **PASSED** |
| **Notifications** | `/notifications` | 22 | Bearer | Pydantic v2 | 200, 201, 404, 422 | `test_notification_delivery_unit.py`| **PASSED** |
| **Analytics & BI** | `/analytics`, `/reports` | 20 | Bearer (Admin) | Pydantic v2 | 200, 403 | `test_dashboard_role_based.py` | **PASSED** |
| **Settings & Audit Logs** | `/settings`, `/audit-logs` | 18 | Bearer (Super Admin) | Pydantic v2 | 200, 201, 403 | `test_05_settings.py` | **PASSED** |

---

### 3. Verification of Core API Behaviors

#### 3.1 Input Validation & Error Handling (HTTP 422 Unprocessable Entity)
When request payloads omit required fields or submit malformed data types, FastAPI automatically validates using Pydantic schemas and returns an explicit HTTP 422 JSON payload:
```json
{
  "detail": [
    {
      "loc": ["body", "email"],
      "msg": "value is not a valid email address",
      "type": "value_error.email"
    }
  ]
}
```

#### 3.2 Authentication Guard Verification (HTTP 401 Unauthorized)
Probing protected endpoints without an `Authorization: Bearer <token>` header returned HTTP 401:
- Tested on `/users/me`: Verified returns `401 Unauthorized` (`detail: Not authenticated`).
- Tested on `/admin/dashboard`: Verified returns `401 Unauthorized`.

#### 3.3 Authorization & Role Enforcement (HTTP 403 Forbidden)
Probing administrative endpoints with a non-admin token (e.g. customer token requesting `/admin/settings`) confirmed that `require_role(["super-admin", "admin"])` dependencies reject the request with `HTTP 403 Forbidden`.

#### 3.4 Rate Limiting & Account Lockout (HTTP 429 & 423)
- **Login Rate Limiting**: The `/auth/login` endpoint is rate limited to 10 requests per 60 seconds per IP address. Exceeding this rate returns `HTTP 429 Too Many Requests`.
- **Account Lockout Defense**: Submitting 5 consecutive invalid passwords triggers account lockout, setting `locked_until` in the database and returning `HTTP 423 Locked`. Verified in `test_02_auth.py::test_login_repeated_bad_passwords_lock_the_account`.
