# Chapter 04 — Backend Production Readiness

## 1. Engine & Runtime Configuration

The backend application (`tourvaa-admin-backend`) runs on **FastAPI 0.139.2** (locked in `requirements.txt`; upgraded from initial 0.115 baseline) and Python 3.12, managed by Starlette and Uvicorn.

### Key Production Subsystems Verified:
1. **API Router Registration**: The central registry in [app/api/router.py](../../tourvaa-admin-backend/app/api/router.py) imports 50 unique router source modules and mounts 64 router instances under `/api` (including intentional aliases and public routers). The 51 physical files in `app/routers/` are a separate filesystem count; `affiliate_redirect.py` is not centrally registered.
2. **Database Engine & Session Management**: SQLAlchemy connection pooling with engine recycling, ping-on-connect, and explicit `except Exception: db.rollback()` generator safeguards.
3. **Middleware Pipeline**:
   - `ApiNoStoreMiddleware`: Disables client caching on dynamic `/api` responses.
   - `CsrfMiddleware`: Enforces double-submit CSRF cookie checks on mutating methods for browser sessions.
   - `CORSMiddleware`: Restricts cross-origin requests to configured domains (`ALLOWED_ORIGINS`).
4. **Lifespan Startup Hooks**:
   - `validate_database_migration_head()`: Halts startup immediately if database schema diverges from code head.
   - `warn_if_redis_unconfigured()`: Flags distributed lock fallback if Redis is unconfigured.
   - `run_seed()`: Seeds initial roles, permissions, and super-admin credentials if database is empty.
   - `_app.openapi()`: Pre-computes OpenAPI schema in memory to guarantee <5ms response latency.
   - `start_background_jobs()`: Spawns 12 async background tasks for booking expiration, report schedules, balance reminders, and payment capture loops.

---

## 2. Multi-Worker Concurrency & Redis Requirement

In single-container or local environments, Uvicorn runs with `WEB_CONCURRENCY=1`.
When scaling horizontally to multiple workers or Kubernetes pods:
- `REDIS_URL` **must be configured**.
- [app/utils/distributed_lock.py](../../tourvaa-admin-backend/app/utils/distributed_lock.py) requires Redis to synchronize background task sweeps across pods.
- [app/services/messaging_ws.py](../../tourvaa-admin-backend/app/services/messaging_ws.py) utilizes Redis PubSub to broadcast chat messages across multiple server processes.

Startup validation in `app.main.validate_worker_concurrency()` will actively block startup if `WEB_CONCURRENCY > 1` without `REDIS_URL`.
