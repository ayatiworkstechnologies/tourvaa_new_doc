# 06 — Backend Architecture & Service Layer Design

## 1. Application Architecture

The backend is built with **FastAPI 0.139.2** (locked in `requirements.txt`; upgraded from initial 0.115 baseline) running on **Python 3.12**. It uses an asynchronous service layer backed by SQLAlchemy 2.0 ORM and PyMySQL.

---

## 2. Startup Lifecycle & Production Verification (`_lifespan`)

FastAPI's async lifespan context manager in [`app/main.py`](../tourvaa-admin-backend/app/main.py) enforces strict startup safety gates:
1. **`validate_database_migration_head()`**: Compares running database heads against Alembic code heads. Aborts if migrations are pending.
2. **`validate_production_config()`**: In production (`APP_ENV != "development"`), ensures debug is disabled, JWT secrets are >= 32 characters, and webhook secrets are present.
3. **`validate_worker_concurrency()`**: Enforces that `REDIS_URL` is set whenever `WEB_CONCURRENCY > 1`.
4. **`validate_pdf_rendering_dependencies()`**: Verifies that ReportLab and Pillow are functional before accepting traffic.
5. **`run_seed()`**: Seeds default roles, permissions, and email templates if missing.
6. **`start_background_jobs()`**: Launches asynchronous worker coroutines with distributed locks.

---

## 3. Middleware Stack

Requests pass through four specialized middlewares:
1. **CORS Middleware**: Validates allowed origins against `ALLOWED_ORIGINS` (wildcards prohibited in production).
2. **ApiNoStore Middleware**: Emits `Cache-Control: no-store` to prevent caching of sensitive customer or financial data.
3. **CsrfMiddleware**: Defends against cross-site request forgery by validating `Origin` and `Referer` headers on state-mutating HTTP methods.
4. **Error Handlers**: Traps validation errors (`RequestValidationError`) and internal exceptions, formatting them into standardized JSON error responses.

---

## 4. Background Job Coroutines

12 background tasks run concurrently within the FastAPI event loop, acquiring distributed locks via Redis (`app/utils/distributed_lock.py`):
- `_expire_stale_bookings_loop`: Sweeps every 15 minutes; releases unpaid seats held longer than 60 minutes.
- `_payment_hold_loop`: Sweeps every 60 minutes; releases pre-authorization card holds exceeding the 4-day supplier decision window.
- `_payment_capture_retry_loop`: Sweeps every 15 minutes; retries failed captures on confirmed bookings.
- `_email_retry_loop`: Sweeps every 15 minutes; retries failed lifecycle emails using exponential backoff (1m, 5m, 25m).
- `_push_retry_loop`: Sweeps every 15 minutes; retries failed WebPush deliveries.
- `_balance_due_reminder_loop`: Sweeps every 60 minutes; dispatches payment reminders for upcoming booking balances.
- `_tour_availability_reminder_loop`: Sweeps every 60 minutes; alerts suppliers when tour departure schedules are nearing expiration.
- `_wishlist_reminder_loop`: Sweeps every 24 hours; notifies customers of seat availability on wishlisted tours.
- `_chat_retention_loop`: Sweeps every 24 hours; purges chat logs older than 90 days.
- `_data_retention_loop`: Sweeps every 24 hours; prunes stale user sessions and email delivery logs.
