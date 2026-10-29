# Chapter 05 — Database Migration Readiness

## 1. Migration History & Current Head

Database migrations for the Tourvaa platform are managed via **Alembic**.

### Migration State Summary
- **Current Head Migration**: [alembic/versions/20261028_0054_financial_document_snapshots.py](../../tourvaa-admin-backend/alembic/versions/20261028_0054_financial_document_snapshots.py)
- **Total Migrations Tracked**: 118 revision files.
- **Pending Migrations for Step 7 Fixes**: **0 (None)**.
- **Verification Rule**: In `app/main.py`, the `validate_database_migration_head()` function executes during the application lifespan and checks `alembic_version` against the migration tree. If any pending migrations exist, the backend will fail to boot with an explicit error.

---

## 2. Table Schema Compatibility & Integrity

The canonical source-level inventory records 138 ORM application tables; a deployed MySQL schema also contains Alembic's `alembic_version` table. The live physical count must still be checked against the target database immediately before migration.
Key structural guarantees verified:
1. **Foreign Key Integrity**: All foreign key relationships (`bookings.customer_id`, `tours.supplier_id`, `invoices.booking_id`, etc.) use explicit `ON DELETE` constraints to prevent orphaned records.
2. **Unique Constraints**: Unique indexes protect user emails, role slugs, booking reference numbers, and voucher codes.
3. **Transaction Safety**: All database operations executed via FastAPI dependency injection use the protected `get_db()` session generator, ensuring automatic rollback on unhandled exceptions.

---

## 3. Database Migration Deployment Runbook

When deploying migrations to a new environment or staging cluster:

```bash
# 1. Use a protected MySQL defaults file or mounted secret; never pass passwords in argv.
# Example defaults file: /run/secrets/tourvaa-mysql.cnf (mode 0600)
mysqldump --defaults-extra-file=/run/secrets/tourvaa-mysql.cnf --single-transaction --routines --triggers tourvaa > pre_migration_backup.sql

# 2. Check current database revision vs head
python -m alembic current
python -m alembic heads

# 3. Apply pending migrations
python -m alembic upgrade head

# 4. Verify head matches code
python -m alembic current --check-heads
```

### Critical Rollback Strategy & MySQL Non-Transactional DDL Limitation
> [!CAUTION]
> **MySQL InnoDB Non-Transactional DDL**: In MySQL (including 8.0 and 8.4), DDL statements (`CREATE TABLE`, `ALTER TABLE`, `DROP TABLE`, `CREATE INDEX`, `DROP INDEX`) execute with **implicit commits** before and after execution. Multi-statement migrations do **NOT** execute inside an atomic rollback transaction.

If an Alembic migration script fails halfway (e.g. the 2nd `ALTER TABLE` statement fails):
1. **Partial Application State**: The 1st statement remains committed in the database, while subsequent statements have not run.
2. **Alembic Version Status**: Alembic does NOT update `alembic_version` on a failed migration; the database remains registered at the previous revision.
3. **Automatic Rollback Failure**: Re-running `alembic upgrade head` or `alembic downgrade` will fail because the partially applied changes are already present.

#### Required Recovery Procedures for Failed Migrations:
- **Approach A (Recommended — Full Restoration)**:
  Restore the database immediately from the pre-migration snapshot:
  ```bash
  mysql --defaults-extra-file=/run/secrets/tourvaa-mysql.cnf tourvaa < pre_migration_backup.sql
  ```
- **Approach B (Forensic Manual DDL Reversal)**:
  If restoring a large database is prohibitive, inspect the failed migration script, identify which statements succeeded, and manually execute the corresponding reverse DDL (e.g., `ALTER TABLE table DROP COLUMN col;`) in the MySQL CLI before investigating the root cause and re-running the migration.
