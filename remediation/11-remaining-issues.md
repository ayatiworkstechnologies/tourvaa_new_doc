# Chapter 11 — Remaining Issues & Deferred Items

## 1. Safety Invariant for Architectural Changes

Under the master instructions:
> "Never modify working modules unnecessarily. Do not attempt to implement every enhancement, speculative risk, or optional recommendation from the improvement roadmap. Focus first on confirmed defects."

Two architectural improvement items identified in the Step 6 inventory were carefully reviewed and deliberately deferred to future development phases.

---

## 2. Inventory of Deferred Architectural Items

### BUG-003: Modularize `app/api/bookings.py` into `BookingService`
- **Module**: Backend Bookings API
- **Current State**: `app/api/bookings.py` is an extensive module (1,200+ lines) handling validation, status transitions, database queries, and notifications inline within route handlers.
- **Working Status**: The module is fully functional, passes all booking lifecycle tests, and correctly executes database transactions.
- **Why Deferred**: Refactoring 1,200 lines of working booking logic into an external service layer constitutes a major architectural rewrite with high regression risk. Modifying it without a confirmed functional failure violates the primary mandate of Step 7.
- **Recommended Roadmap**:
  1. Define a strict `BookingService` interface in `app/services/booking_service.py`.
  2. Implement unit tests asserting each status transition (`PENDING` -> `CONFIRMED` -> `CANCELLED`).
  3. Migrate route handlers one by one in a dedicated, isolated release.

---

### BUG-004: Cloud Object Storage Migration (Local `/uploads` to S3/Cloudflare R2)
- **Module**: File Uploads & Media Management
- **Current State**: Documents and tour images are written to a local server directory (`/uploads`).
- **Working Status**: Local disk storage functions reliably in single-instance and development deployments.
- **Why Deferred**: Migrating to AWS S3 or Cloudflare R2 requires external infrastructure provisioning, IAM credentials, bucket policy definitions, and CDN configuration outside the local codebase.
- **Recommended Roadmap**:
  1. Implement a storage abstraction (`app/storage/base.py`) supporting local filesystem and S3 backends via `boto3`.
  2. Configure environment variables (`S3_BUCKET`, `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`).
  3. Create an automated migration script to upload existing local files to the bucket before switching production traffic.

---

## 3. Risk Assessment of Deferred Items

| Item | Current Risk Level | Operational Mitigation |
|:---|:---:|:---|
| BUG-003 (Booking Service Refactor) | Low | Existing automated tests continuously guard booking endpoints against regressions. |
| BUG-004 (Cloud Storage Migration) | Low-Medium | In containerized multi-pod deployments, persistent volume claims (PVCs) can mount `/uploads` until S3 is provisioned. |
