# Module 06: Invoices & Financial Confirmation Receipts

## 1. Module Overview

| Attribute | Details |
|---|---|
| **Module Name** | Invoices & Financial Confirmation Receipts |
| **Business Purpose** | Generates PDF invoices, handles GST/tax calculations, tracks partial/deposit balance due dates, sends balance reminders, and issues immutable confirmation receipts. |
| **Supported Roles** | Customers, Agents, Suppliers, Admins |
| **Permissions Required** | `invoices.view, invoices.create, invoices.edit` |

---

## 2. Functional & Business Workflows

### 2.1 Workflow Architecture
```mermaid
flowchart LR
    BOOKING[Confirmed Booking] --> INVOICE[Generate Invoice with Tax / GST]
    BOOKING --> RECEIPT[Generate Confirmation Receipt PDF]
    INVOICE --> REMIND[Balance Due Reminders (60m loop)]
    RECEIPT --> DOWNLOAD[Customer / Agent Downloads from Portal]
```

### 2.2 Functional Capabilities
- **Core Operations**: Fully implemented CRUD lifecycle operations backing the portal interfaces.
- **Validation Rules**: Strict Pydantic and React Hook Form validation rules enforcing data integrity and sanitization.
- **Error Handling**: Standardized error responses returning structured JSON codes and human-readable messages.

---

## 3. Technical Implementation Details

### 3.1 Source Files & Entry Points
- **Frontend Pages**:
- [`/customer/invoices`](../../tourvaa-admin-frontend/src/app/customer/invoices/page.tsx)
- [`/agent/invoices`](../../tourvaa-admin-frontend/src/app/agent/invoices/page.tsx)
- [`/supplier/invoices`](../../tourvaa-admin-frontend/src/app/supplier/invoices/page.tsx)
- [`/admin/invoices`](../../tourvaa-admin-frontend/src/app/admin/invoices/page.tsx)
- [`/admin/invoice-templates`](../../tourvaa-admin-frontend/src/app/admin/invoice-templates/page.tsx)
- **Backend Routers**:
- [`app/routers/invoices.py`](../../tourvaa-admin-backend/app/routers/invoices.py)
- [`app/routers/private_documents.py`](../../tourvaa-admin-backend/app/routers/private_documents.py)
- **Domain Services**:
- [`app/services/invoices.py`](../../tourvaa-admin-backend/app/services/invoices.py)
- [`app/services/confirmation_receipts.py`](../../tourvaa-admin-backend/app/services/confirmation_receipts.py)

### 3.2 Database Entities
- **Primary Database Tables**:
- `invoices`
- `invoice_items`
- `bookings`
- `payments`
