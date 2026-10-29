# Chapter 14: Known Issues, Technical Debt & Pending Work

## 1. Traceability Register of Audit Findings

The table below maintains strict traceability to the verified findings documented in Chapters 26 through 33 of the technical audit:

| Issue ID | Domain / Module | Priority | Description | Remediation Plan | Audit Reference |
|---|---|---|---|---|---|
| **SEC-01** | Security / Auth | **P0** | CSRF middleware skips check when `tourvaa_csrf` cookie is omitted. | Require CSRF token for all state-changing requests carrying session cookies. | [`Chapter 29: SEC-01`](../29-security-gap-analysis.md) |
| **DB-01** | Database Engine | **P0** | `get_db()` lacks explicit rollback on exception, risking connection pool dirty states. | Add `except Exception: db.rollback(); raise` in `get_db()`. | [`Chapter 27: 1.1`](../27-backend-database-audit.md) |
| **SEC-02** | Security / Access | **P0** | `_ensure_booking_access` permits access when `actor=None`. | Enforce `if actor is None: raise HTTPException(401)`. | [`Chapter 29: SEC-02`](../29-security-gap-analysis.md) |
| **ARCH-01**| Code Quality | **P1** | `app/services/bookings.py` is 4,188 lines of mixed domain logic. | Modularize into `pricing.py`, `lifecycle.py`, `supplier_ops.py`, `documents.py`. | [`Chapter 27: 1.2`](../27-backend-database-audit.md) |
| **OPS-01** | DevOps / Deploy | **P1** | `docker-entrypoint.sh` executes migrations automatically on container startup. | Set `RUN_MIGRATIONS=false` in app containers; run migrations via dedicated CI task. | [`Chapter 30: 2.1`](../30-production-readiness-audit.md) |
| **OPS-02** | Infrastructure | **P1** | Uploads write to local disk `/data/storage` (ephemeral container risk). | Implement S3-compatible cloud object storage abstraction (AWS S3, MinIO). | [`Chapter 30: 2.2`](../30-production-readiness-audit.md) |
| **TEST-01**| QA / Concurrency| **P1** | Missing multi-threaded concurrency race condition test for seat holds. | Implement Pytest concurrency test simulating simultaneous checkouts. | [`Chapter 31: TS-01`](../31-testing-coverage-gaps.md) |
| **DB-02** | Performance | **P2** | Unindexed foreign keys (`bookings.booking_source`, `payment_transactions.gateway_reference_id`). | Add Alembic migration with secondary B-tree indexes. | [`Chapter 27: 2.2`](../27-backend-database-audit.md) |
| **PERF-01**| Performance | **P2** | Synchronous file I/O in async endpoints in `uploads.py` and `cms.py`. | Migrate disk writes to `aiofiles` or `run_in_threadpool`. | [`Chapter 27: 1.3`](../27-backend-database-audit.md) |
| **UI-01** | Frontend UX | **P2** | Customer portal bookings table lacks an inline "Write a Review" modal. | Add review modal trigger on completed bookings in `/customer/bookings`. | [`Chapter 26: 2.1`](../26-functional-gap-analysis.md) |
