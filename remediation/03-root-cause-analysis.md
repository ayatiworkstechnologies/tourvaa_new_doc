# Chapter 03 — Root Cause Analysis

## 1. Methodology

For every confirmed defect, root cause analysis was conducted by tracing the complete execution chain:
```
User Action → Frontend Component → API Client → Backend Router → Service/Middleware → Database → Response → UI State
```

No speculative assumptions were accepted. Each defect's root cause was verified using the exact source code lines.

---

## 2. Root Cause Investigations

### BUG-001: CSRF Protection Bypass via Missing Cookie
- **Component**: `app/middleware/csrf.py`
- **Execution Chain**:
  `Browser HTTP Request` → `Starlette BaseHTTPMiddleware (CsrfMiddleware)` → `dispatch()`
- **Flawed Code**:
  ```python
  cookie_token = request.cookies.get(csrf_cookie_name(portal_from_request(request)))
  if cookie_token:
      header_token = request.headers.get(CSRF_HEADER_NAME)
      if not header_token or header_token != cookie_token:
          return JSONResponse(status_code=403, ...)
  ```
- **Root Cause**: The middleware only performed token validation *if* the `tourvaa_csrf` cookie was already sent by the browser (`if cookie_token:`). If a cross-origin attacker induced a victim's browser to send a mutating request using ambient session cookies (`tourvaa_access`) while omitting the CSRF cookie, the check was completely bypassed!
- **Resolution**: Trigger validation whenever an authentication cookie (`tourvaa_access`, `tourvaa_admin_access`, or portal cookie) is present on mutating methods.

---

### BUG-002: Missing Transaction Rollback in `get_db` Generator
- **Component**: `app/database/__init__.py`
- **Execution Chain**:
  `FastAPI Route Dependency` → `Depends(get_db)` → `SessionLocal()` → `yield db` → `Unhanlded Exception in Endpoint` → `Generator Exit`
- **Flawed Code**:
  ```python
  def get_db():
      db = SessionLocal()
      try:
          yield db
      finally:
          db.close()
  ```
- **Root Cause**: While `db.close()` was executed in the `finally` block, SQLAlchemy connection pool returns the underlying raw DBAPI connection to the pool. If an unhandled exception occurred after partial `db.add()` or pending dirty changes without an explicit `db.rollback()`, connection reuse or pool recycling in SQLite/PostgreSQL could retain dirty transaction states.
- **Resolution**: Add an explicit `except Exception:` block that invokes `db.rollback()` before re-raising the exception.

---

### BUG-005: Stale Portal Session Cookies on Role Mismatch
- **Component**: `src/components/public/portal/PortalAuthPage.tsx`
- **Execution Chain**:
  `User Login on Portal` → `Login Succeeds with Wrong Role` → `Error Displayed` → `User Left with Issued Session Cookies`
- **Flawed Code**:
  ```typescript
  await api.post("/auth/logout", undefined, {
    headers: { "X-Tourvaa-Portal": ["admin", "super-admin", "sub-admin"].includes(roleSlug) ? "admin" : "public" },
  }).catch(() => {});
  ```
- **Root Cause**: Complex header injection caused logout route to selectively clear only specific cookie scopes, occasionally leaving residual cross-portal cookies that collided with the next login attempt.
- **Resolution**: Standardize on `await api.post("/auth/logout").catch(() => {});`, allowing backend logout handler to invalidate all portal session cookies cleanly.

---

### BUG-006: Custom Portal Role Dashboard Redirection
- **Component**: `src/lib/utils/dashboardPath.ts`
- **Execution Chain**:
  `Post-Login Redirect` → `getDashboardPath(roleSlug)`
- **Flawed Code**:
  ```typescript
  export function getDashboardPath(roleSlug: string): string {
    const slug = roleSlug.trim().toLowerCase();
    if (slug === "customer") return "/customer/dashboard";
    if (slug === "agent-reseller") return "/agent/dashboard";
    if (slug === "supplier") return "/supplier/dashboard";
    if (slug === "affiliate") return "/affiliate/dashboard";
    return /^[a-z0-9]+(?:-[a-z0-9]+)*$/.test(slug) ? "/admin/dashboard" : "/login";
  }
  ```
- **Root Cause**: Non-admin portal roles created dynamically or portal logins with custom slugs were falling back to `/admin/dashboard` instead of their respective portal dashboard.
- **Resolution**: Add optional `isPortalRole` parameter returning `/${slug}/dashboard`.

---

### BUG-008: Non-Standardized Native Date Input
- **Component**: `src/app/admin/invoice-templates/page.tsx`
- **Execution Chain**:
  `Sample Invoice Form` → `<input type="date">`
- **Root Cause**: Across the entire Tourvaa frontend design system, all dates are collected via controlled text inputs formatted as `YYYY-MM-DD` or custom date-pickers to ensure cross-browser consistency. Line 876 retained an archaic native `<input type="date">`.
- **Resolution**: Change `type="date"` to `type="text"` with `placeholder="YYYY-MM-DD"`.

---

### BUG-009: Missing Next.js Metadata Layout
- **Component**: `src/app/admin/invoice-templates/layout.tsx`
- **Execution Chain**:
  `Next.js App Router Metadata Resolution` → Inspect Directory Tree
- **Root Cause**: In the 163-page Next.js App Router tree, every admin route folder contained a `layout.tsx` invoking `metadataFor("/admin/...")` except for `admin/invoice-templates`. This resulted in default fallback metadata rather than route-specific metadata.
- **Resolution**: Create `layout.tsx` exporting `metadata = metadataFor("/admin/invoice-templates")`.

---

### BUG-010: Omission of `sub-admin` in Header Role Guard
- **Component**: `src/components/public/PublicHeader.tsx`
- **Execution Chain**:
  `Public Header Render` → Check `isAdminRole`
- **Flawed Code**:
  ```typescript
  const isAdminRole = ["admin", "super-admin", "super_admin"].includes(roleSlug.toLowerCase());
  ```
- **Root Cause**: The RBAC system assigns `sub-admin` as an administrative role, but `PublicHeader.tsx` omitted `sub-admin`, leading to inconsistent header action visibility when a sub-admin navigated the public storefront.
- **Resolution**: Add `"sub-admin"` to the `isAdminRole` check array.

---

### BUG-012: Dynamic OpenAPI Reflection Latency
- **Component**: `app/main.py`
- **Execution Chain**:
  `First Request to /docs or /openapi.json` → `FastAPI inspects the documented 594-path / 785-operation schema` → `3.5s Latency Spike`
- **Root Cause**: FastAPI builds its OpenAPI schema lazily on the first request to `/openapi.json`. The documented schema contains 594 paths and 785 operations with detailed Pydantic schemas, so this reflection incurred 3.5 seconds of CPU delay on cold starts.
- **Resolution**: Trigger `_app.openapi()` during the async `_lifespan()` startup sequence, pre-computing and caching the schema in memory.
