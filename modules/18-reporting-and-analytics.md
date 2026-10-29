# Module 18: Reporting & Business Analytics

## 1. Module Overview

| Attribute | Details |
|---|---|
| **Module Name** | Reporting & Business Analytics |
| **Business Purpose** | Comprehensive financial and operational reporting generating sales summaries, supplier payouts reconciliation, agent commissions, and scheduled automated reports. |
| **Supported Roles** | Admins, Super Admins, Suppliers (own reports) |
| **Permissions Required** | `reports.view, reports.create, supplier_ledger.view, agent_ledger.view` |

---

## 2. Functional & Business Workflows

### 2.1 Workflow Architecture
```mermaid
flowchart TD
    SCHED[Report Schedule: Daily / Weekly / Monthly] --> SWEEP[_report_schedule_loop (60m)]
    SWEEP --> QUERY[Query Aggregated Sales, Invoices & Commissions]
    QUERY --> EXCEL[Generate OpenPyXL Spreadsheet]
    EXCEL --> EMAIL[Dispatch to Admin / Financial Stakeholders]
```

### 2.2 Functional Capabilities
- **Core Operations**: Fully implemented CRUD lifecycle operations backing the portal interfaces.
- **Validation Rules**: Strict Pydantic and React Hook Form validation rules enforcing data integrity and sanitization.
- **Error Handling**: Standardized error responses returning structured JSON codes and human-readable messages.

---

## 3. Technical Implementation Details

### 3.1 Source Files & Entry Points
- **Frontend Pages**:
- [`/admin/reports`](../../tourvaa-admin-frontend/src/app/admin/reports/page.tsx)
- [`/admin/reports/create`](../../tourvaa-admin-frontend/src/app/admin/reports/create/page.tsx)
- [`/supplier/reports`](../../tourvaa-admin-frontend/src/app/supplier/reports/page.tsx)
- **Backend Routers**:
- [`app/routers/reports.py`](../../tourvaa-admin-backend/app/routers/reports.py)
- **Domain Services**:
- [`app/services/reports.py`](../../tourvaa-admin-backend/app/services/reports.py)

### 3.2 Database Entities
- **Primary Database Tables**:
- `report_schedules`
- `bookings`
- `payments`
- `supplier_ledgers`
- `agent_ledger`
