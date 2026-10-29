# Module 19: Audit Logging & Platform Governance

## 1. Module Overview

| Attribute | Details |
|---|---|
| **Module Name** | Audit Logging & Platform Governance |
| **Business Purpose** | Provides immutable compliance audit trails, capturing actor IDs, IP addresses, entity mutations, before/after JSON diffs, login successes/failures, and session revocations. |
| **Supported Roles** | Admins, Super Admins |
| **Permissions Required** | `activity_logs.view, audit_logs.view` |

---

## 2. Functional & Business Workflows

### 2.1 Workflow Architecture
```mermaid
flowchart LR
    ACTION[Admin / Partner Mutation] --> LOG[log_audit(db, action, entity, before, after)]
    LOG --> DB_AUDIT[(audit_logs Table - Immutable)]
    LOGIN[Login Attempt] --> DB_LOGIN[(login_history Table)]
    DB_AUDIT -. Deliberately Excluded from Retention Pruning .-> COMPLIANCE[Long-term Compliance Record]
```

### 2.2 Functional Capabilities
- **Core Operations**: Fully implemented CRUD lifecycle operations backing the portal interfaces.
- **Validation Rules**: Strict Pydantic and React Hook Form validation rules enforcing data integrity and sanitization.
- **Error Handling**: Standardized error responses returning structured JSON codes and human-readable messages.

---

## 3. Technical Implementation Details

### 3.1 Source Files & Entry Points
- **Frontend Pages**:
- [`/admin/activity-logs`](../../tourvaa-admin-frontend/src/app/admin/activity-logs/page.tsx)
- [`/admin/audit-logs`](../../tourvaa-admin-frontend/src/app/admin/audit-logs/page.tsx)
- **Backend Routers**:
- [`app/routers/audit.py`](../../tourvaa-admin-backend/app/routers/audit.py)
- **Domain Services**:
- [`app/services/audit.py`](../../tourvaa-admin-backend/app/services/audit.py)
- [`app/services/retention.py`](../../tourvaa-admin-backend/app/services/retention.py)

### 3.2 Database Entities
- **Primary Database Tables**:
- `audit_logs`
- `login_history`
- `user_status_history`
- `user_sessions`
