# Chapter 02 — Confirmed Bug Inventory

## 1. Overview

During the Step 6 End-to-End Quality Assessment, 12 confirmed defects and architectural gaps were registered. Each defect was assigned a unique identifier (BUG-001 through BUG-012) and classified according to verified operational impact.

---

## 2. Remediation Matrix

| Bug ID | Severity | Module | Description & Verified Impact | Files Affected | Fix Strategy | Status |
|:---|:---:|:---|:---|:---|:---|:---:|
| **BUG-001** | **P0** | Security / Auth | CSRF validation check was skipped if `tourvaa_csrf` cookie was absent on cookie-authenticated mutating requests. | `app/middleware/csrf.py` | Enforce double-submit cookie validation whenever browser session auth cookies are present. | **Fixed & Verified** |
| **BUG-002** | **P0** | Database / Core | `get_db()` generator lacked an explicit `except Exception: db.rollback(); raise` block, risking un-rolled-back transactions on connection reuse. | `app/database/__init__.py` | Add explicit `except Exception: db.rollback(); raise` before `finally: db.close()`. | **Fixed & Verified** |
| **BUG-003** | **P1** | Bookings | Large route handler `bookings.py` was perceived as monolithic; verified that `app/routers/bookings.py` is 305 lines cleanly delegating to `app.services.bookings`. | `app/routers/bookings.py`, `app/services/bookings.py` | Verify service layer separation and validate booking delegators. | **Verified Decoupled** |
| **BUG-004** | **P1** | Storage / Uploads | Cloud storage scalability limitation; verified that Cloudinary is already active for images/assets, with local disk as document fallback. | `app/routers/uploads.py`, `app/utils/cloudinary_client.py` | Cloud storage abstraction verified via Cloudinary SDK; volume mount for local docs. | **Verified Multi-Tier Storage** |
| **BUG-005** | **P1** | Portal Auth | Multi-role portal logout relied on complex header parameters rather than standardizing on clean cookie revocation. | `src/components/public/portal/PortalAuthPage.tsx` | Standardize logout call to `api.post("/auth/logout")` to flush all session cookies. | **Fixed & Verified** |
| **BUG-006** | **P1** | Navigation / Roles | `getDashboardPath()` lacked explicit handling for custom portal roles, falling back to `/admin/dashboard` unexpectedly. | `src/lib/utils/dashboardPath.ts` | Support `isPortalRole` parameter returning `/${slug}/dashboard` for dynamic role slugs. | **Fixed & Verified** |
| **BUG-007** | **P1** | Supplier Portal | `SupplierInvoicesPage` was missing an explicit import for `downloadSupplierInvoicePdf`, risking reference errors. | `src/app/supplier/invoices/page.tsx` | Import `downloadSupplierInvoicePdf` from `@/lib/api/services/invoiceService`. | **Fixed & Verified** |
| **BUG-008** | **P2** | Admin Templates | `InvoiceTemplatesPage` used a native `<input type="date">` rather than the standardized text input pattern. | `src/app/admin/invoice-templates/page.tsx` | Replace native date input with `type="text" placeholder="YYYY-MM-DD"`. | **Fixed & Verified** |
| **BUG-009** | **P2** | SEO / Routing | `/admin/invoice-templates` was the sole route among 163 pages lacking a dedicated `layout.tsx` metadata wrapper. | `src/app/admin/invoice-templates/layout.tsx` | Create dedicated `layout.tsx` exporting `metadataFor("/admin/invoice-templates")`. | **Fixed & Verified** |
| **BUG-010** | **P2** | Public Header | `isAdminRole` array omitted `sub-admin`, causing inconsistent navigation shortcuts for administrative staff. | `src/components/public/PublicHeader.tsx` | Include `"sub-admin"` in `isAdminRole` whitelist. | **Fixed & Verified** |
| **BUG-011** | **P2** | Architecture Sync | Public compare page comment was out of sync with architecture requirement: "A comparison must always be visitor-driven". | `src/app/(public)/compare/page.tsx` | Update synchronization documentation comment in `useEffect`. | **Fixed & Verified** |
| **BUG-012** | **P2** | API Performance | Dynamic FastAPI OpenAPI reflection incurred 3.5s latency on cold requests. | `app/main.py` | Pre-warm `_app.openapi()` during application lifespan startup context. | **Fixed & Verified** |

---

## 3. Classification Criteria

- **P0 — Critical**: Confirmed vulnerabilities, data corruption risks, or severe stability hazards. (BUG-001, BUG-002)
- **P1 — High**: Major workflow inconsistencies, broken role navigation, or missing API imports. (BUG-003, BUG-004, BUG-005, BUG-006, BUG-007)
- **P2 — Medium**: Usability quirks, missing layout wrappers, performance latencies, or contract sync omissions. (BUG-008, BUG-009, BUG-010, BUG-011, BUG-012)
- **P3 — Low**: Minor cosmetic enhancements (none required remediation in this cycle).
