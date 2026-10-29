# Chapter 15 — Open Risks & Architectural Limitations

## 1. Documented Architectural Debt & Deferred Items

In accordance with strict safety rules, operational enhancements that did not represent broken functionality were deferred to protect codebase stability during release candidate preparation.

---

## 2. Detailed Limitation Descriptions

### 1. BUG-003: Monolithic `bookings.py` Route Handler
- **Description**: `app/api/bookings.py` handles route definitions, data validation, database queries, and notifications within a single 1,200+ line file.
- **Operational Risk**: Low. The module is fully functional, thoroughly covered by automated test suites, and enforces correct database transaction boundaries.
- **Mitigation**: Maintain existing test coverage until a dedicated architectural refactoring sprint extracts a decoupled `BookingService`.

### 2. BUG-004: Local Filesystem Storage (`/uploads`)
- **Description**: Media uploads and tour documents are saved to a mounted local directory (`/data/storage/uploads`) rather than AWS S3 or Cloudflare R2.
- **Operational Risk**: Medium in multi-container setups. Without a shared Persistent Volume Claim (PVC), files uploaded to Pod A would not be immediately visible on Pod B.
- **Mitigation**: Deploy with a single backend replica or mount a shared NFS/EFS persistent volume to `/data` until the S3 storage adapter is implemented.

### 3. Redis Dependency for Horizontal Scaling
- **Description**: Single-worker deployments run fine without Redis. However, running `WEB_CONCURRENCY > 1` requires Redis for sweep locking and WebSocket messaging.
- **Operational Risk**: Low if documented. Startup validation blocks multi-worker boots if Redis is missing.
- **Mitigation**: Configure `REDIS_URL` in production container definitions.
