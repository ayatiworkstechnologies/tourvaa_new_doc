# 19 — Technical Debt & Architectural Review

## 1. Technical Debt Register

| ID | Severity | Area | Observation & Evidence | Technical Debt Impact | Recommended Remediation |
|---|---|---|---|---|---|
| **TD-01** | **Medium** | Backend Services | High line count in `app/services/bookings.py` (>4,000 lines). | Centralizes booking creation, seat quota checks, status transitions, and emails in a single large file. | Refactor into smaller sub-modules: `booking_creation.py`, `booking_state_machine.py`, `booking_commercials.py`. |
| **TD-02** | **Low** | Frontend Proxy | Trailing-slash normalization handled manually in `src/proxy.ts`. | Required because `skipTrailingSlashRedirect: true` in `next.config.ts`. | Consolidate slash normalization once Next.js rewrite routing matures. |
| **TD-03** | **Low** | Database Schema | Historical migration drift handled via reconciliation script. | Alembic has 170 migrations; new database spin-up takes multiple minutes to run sequentially. | Create a consolidated migration baseline (`squash_migrations.py`) for clean future setups while preserving legacy migrations. |
