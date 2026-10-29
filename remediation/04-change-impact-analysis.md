# Chapter 04 — Change Impact Analysis

## 1. Upstream & Downstream Dependency Evaluation

Before modifying any source code, full dependency mapping was performed across all affected files to ensure zero regressions in dependent modules.

---

## 2. Component Dependency Analysis

### 1. `app/database/__init__.py`
- **Consumers**: Every backend router (`app/api/*.py`), background jobs (`app/jobs/*.py`), and seed runners (`app/database/seed.py`).
- **Potential Risk**: Introducing extra overhead or altering session yields could break endpoint dependency injection.
- **Impact Mitigation**: The change modifies only the error handling path (`except Exception: db.rollback(); raise`). Normal successful requests experience zero behavioral change.

### 2. `app/middleware/csrf.py`
- **Consumers**: All HTTP requests routed through FastAPI.
- **Potential Risk**: Legitimate API clients (such as mobile applications or integration tests using `Authorization: Bearer <token>`) might be blocked if CSRF checks were applied universally.
- **Impact Mitigation**: Bearer-token requests without auth cookies bypass the check, preserving full compatibility for API clients, mobile apps, and automated integration test suites.

### 3. `app/main.py`
- **Consumers**: Application startup lifecycle.
- **Potential Risk**: Failure during OpenAPI generation could abort startup.
- **Impact Mitigation**: Wrapped inside `try...except Exception as e: logger.warning(...)` to guarantee that startup continues smoothly even if schema generation fails.

### 4. `src/lib/utils/dashboardPath.ts`
- **Consumers**: `src/components/public/portal/PortalAuthPage.tsx`, `src/app/login/page.tsx`, and auth route guards.
- **Potential Risk**: Altering default admin dashboard paths could misroute existing administrative logins.
- **Impact Mitigation**: Default parameter `isPortalRole = false` preserves the exact original return value (`/admin/dashboard`) for all existing invocations.

### 5. `src/components/public/PublicHeader.tsx`
- **Consumers**: Public storefront header across all client-facing pages.
- **Potential Risk**: Altering visitor navigation or customer shopping cart controls.
- **Impact Mitigation**: The edit merely adds `"sub-admin"` to the administrative exclusion list, ensuring sub-admin back-office accounts do not show customer shopping controls. Customer and guest visitor behavior remains completely unchanged.

---

## 3. Invariant Verification

| Module | Tested Behavior | Verification Mechanism | Result |
|:---|:---|:---|:---:|
| Core API Routing | Tested core routes respond with expected schemas; the documented OpenAPI surface is 594 paths / 785 operations | `pytest tests/test_01_core_health.py` | Preserved within the recorded test scope |
| Authentication Flow | Login, lockout, refresh, and profile endpoints | `pytest tests/test_02_auth.py` | Preserved |
| Frontend Navigation | 30 key route paths exist and render | Node test `module-routes.test.mjs` | Preserved |
| SEO Metadata Tree | 163 Next.js pages export valid metadata | Node test `metadata-flow.test.mjs` | Preserved |
| TypeScript Types | Zero compile errors across entire codebase | `npx tsc --noEmit` | Clean (0 errors) |
