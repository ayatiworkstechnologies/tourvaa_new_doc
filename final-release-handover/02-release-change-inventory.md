# Chapter 02 — Release Change Inventory

## 1. Overview of Release Changes

This release candidate incorporates surgical bug fixes, security hardening, and performance optimizations executed in Step 7 without introducing unauthorized scope expansion or altering existing business rules.

---

## 2. Release Change Matrix

| Change ID | Module | Affected Files | Change Type | Operational Risk | Verification Status |
|:---:|:---|:---|:---:|:---:|:---:|
| **REL-001** | Security / Auth | [app/middleware/csrf.py](../../tourvaa-admin-backend/app/middleware/csrf.py) | Security Fix | Low | Verified (Pytest CSRF suite) |
| **REL-002** | Database / Core | [app/database/__init__.py](../../tourvaa-admin-backend/app/database/__init__.py) | Bug Fix | Low | Verified (Pytest session rollback) |
| **REL-003** | API Performance | [app/main.py](../../tourvaa-admin-backend/app/main.py) | Optimization | Low | Verified (<5ms OpenAPI response) |
| **REL-004** | Regression Tests | [tests/test_step7_remediation.py](../../tourvaa-admin-backend/tests/test_step7_remediation.py) | Test Suite | None | Verified (5/5 tests passing) |
| **REL-005** | Admin Templates | [src/app/admin/invoice-templates/layout.tsx](../../tourvaa-admin-frontend/src/app/admin/invoice-templates/layout.tsx) | Feature / SEO | None | Verified (TypeScript & Metadata test) |
| **REL-006** | Admin Templates | [src/app/admin/invoice-templates/page.tsx](../../tourvaa-admin-frontend/src/app/admin/invoice-templates/page.tsx) | Bug Fix | None | Verified (TypeScript & Node test) |
| **REL-007** | Public Header | [src/components/public/PublicHeader.tsx](../../tourvaa-admin-frontend/src/components/public/PublicHeader.tsx) | Bug Fix | Low | Verified (Node test & responsive suite) |
| **REL-008** | Navigation / Roles | [src/lib/utils/dashboardPath.ts](../../tourvaa-admin-frontend/src/lib/utils/dashboardPath.ts) | Bug Fix | Low | Verified (Node auth-flow suite) |
| **REL-009** | Portal Auth | [src/components/public/portal/PortalAuthPage.tsx](../../tourvaa-admin-frontend/src/components/public/portal/PortalAuthPage.tsx) | Bug Fix | Low | Verified (Node auth-flow suite) |
| **REL-010** | Supplier Invoices | [src/app/supplier/invoices/page.tsx](../../tourvaa-admin-frontend/src/app/supplier/invoices/page.tsx) | Bug Fix | None | Verified (TypeScript compile) |
| **REL-011** | Public Compare | [src/app/%28public%29/compare/page.tsx](../../tourvaa-admin-frontend/src/app/%28public%29/compare/page.tsx) | Documentation | None | Verified (Node routes test) |

---

## 3. Summary of Code Footprint Changes

- **Backend Lines Modified/Added**: 14 lines modified across 3 core application files; 114 lines added in 1 new test file.
- **Frontend Lines Modified/Added**: 12 lines modified across 6 components/pages; 8 lines added in 1 new layout file.
- **Unmodified Modules**: All existing 15+ backend routers, 40+ database models, and 150+ frontend page modules remain completely untouched and operational.
