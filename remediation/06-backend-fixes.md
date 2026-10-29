# Chapter 06 — Controlled Backend Fixes

## 1. Overview of Backend Remediations

Backend fixes targeted confirmed database transaction integrity, security middleware enforcement, and application startup optimization without breaking existing API contracts.

A total of 3 existing backend files were modified and 1 new regression test file was added to `tourvaa-admin-backend`.

---

## 2. Detailed Backend File Changes

### 1. [app/database/__init__.py](../../tourvaa-admin-backend/app/database/__init__.py)
- **Defect Addressed**: BUG-002 (Missing Transaction Rollback in `get_db`)
- **Change Description**: Added explicit `except Exception: db.rollback(); raise` block in `get_db` generator.
- **Diff**:
```diff
@@ -26,5 +26,8 @@ def get_db():
     db = SessionLocal()
     try:
         yield db
+    except Exception:
+        db.rollback()
+        raise
     finally:
         db.close()
```
- **Rationale**: If an unhandled exception is raised inside an endpoint handler, SQLAlchemy could return the raw connection to the pool with uncommitted dirty states. Explicit rollback guarantees clean connection recycling.

---

### 2. [app/middleware/csrf.py](../../tourvaa-admin-backend/app/middleware/csrf.py)
- **Defect Addressed**: BUG-001 (CSRF Protection Bypass via Missing Cookie)
- **Change Description**: Enforced double-submit cookie validation whenever browser authentication cookies are present on mutating methods.
- **Diff**:
```diff
@@ -1,7 +1,7 @@
 from starlette.middleware.base import BaseHTTPMiddleware
 from starlette.requests import Request
 from starlette.responses import JSONResponse
-from app.auth.cookies import csrf_cookie_name, portal_from_request
+from app.auth.cookies import csrf_cookie_name, portal_from_request, access_cookie_name

 CSRF_HEADER_NAME = "X-CSRF-Token"
 UNSAFE_METHODS = {"POST", "PUT", "PATCH", "DELETE"}
@@ -24,19 +24,23 @@ class CsrfMiddleware(BaseHTTPMiddleware):
-    Enforcement only triggers when the CSRF cookie is actually present...
+    Enforcement triggers whenever browser session cookies are used for
+    mutating requests, preventing attackers from bypassing checks by
+    stripping the CSRF cookie. Bearer-token clients remain unaffected.

     async def dispatch(self, request: Request, call_next):
         if request.method in UNSAFE_METHODS and request.url.path not in EXEMPT_PATHS:
-            cookie_token = request.cookies.get(csrf_cookie_name(portal_from_request(request)))
-            if cookie_token:
+            portal = portal_from_request(request)
+            auth_cookie = (
+                request.cookies.get(access_cookie_name(portal))
+                or request.cookies.get("tourvaa_access")
+                or request.cookies.get("tourvaa_admin_access")
+            )
+            cookie_token = request.cookies.get(csrf_cookie_name(portal))
+            if auth_cookie or cookie_token:
                 header_token = request.headers.get(CSRF_HEADER_NAME)
-                if not header_token or header_token != cookie_token:
+                if not cookie_token or not header_token or header_token != cookie_token:
                     return JSONResponse(
                         status_code=403,
                         content={"status": "error", "message": "CSRF token missing or invalid"},
```
- **Rationale**: Eliminates the critical vulnerability where an attacker could omit the CSRF cookie while transmitting ambient browser auth cookies.

---

### 3. [app/main.py](../../tourvaa-admin-backend/app/main.py)
- **Defect Addressed**: BUG-012 (Dynamic OpenAPI Schema Generation Latency)
- **Change Description**: Pre-computed OpenAPI schema in memory during application lifespan startup.
- **Diff**:
```diff
@@ -703,6 +703,11 @@ async def _lifespan(_app: FastAPI):
     validate_database_migration_head()
     warn_if_redis_unconfigured()
     run_seed()
+    if _docs_enabled:
+        try:
+            _app.openapi()
+        except Exception as e:
+            logger.warning("OpenAPI schema pre-warm failed: %s", e)
     await start_background_jobs()
     try:
         yield
```
- **Rationale**: Eliminates the initial 3.5s CPU reflection delay on cold requests to `/openapi.json` or `/docs`.
