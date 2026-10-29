# 02 — Test Environment Discovery & Baseline Assessment
**Tourvaa Travel & Tourism Experience Platform**

---

### 1. Test Environment Topology

The quality audit was conducted against an active local development environment configured on the host machine. Prior to test execution, a non-invasive port and process scan was performed to confirm service status, baseline connectivity, and safety boundaries.

```
Host Architecture: Windows (Local Workstation)
Host Network Ports:
├── Port 3000: OPEN  [Next.js 14 Frontend Dev Server — PID: 19296]
├── Port 8000: OPEN  [FastAPI Backend / Uvicorn Server — PID: 23632]
├── Port 3306: OPEN  [MySQL Community Server 8.0.46 — System Service]
├── Port 8080: OPEN  [EnterpriseDB / PostgreSQL Secondary Service]
├── Port 5432: OPEN  [PostgreSQL Server]
└── Port 6379: CLOSED [Redis Server (Configured as empty in .env)]
```

---

### 2. Component Configuration & Runtime Baselines

#### 2.1 Frontend Component (`tourvaa-admin-frontend`)
- **Framework**: Next.js 14.2.35 (React 18.2.0, TypeScript 5.4.5)
- **Styling**: Tailwind CSS with custom responsive utilities
- **Runtime Process**: `node.exe` running `npm run dev`
- **Active Base URL**: `http://127.0.0.1:3000`
- **Environment File**: `.env` (API proxy target: `http://localhost:8000`, WebSocket: `ws://localhost:8000`)
- **Test Automation**:
  - Playwright: Configured in `playwright.config.ts` targeting `http://127.0.0.1:3000` with `reuseExistingServer: true`.
  - Vitest: Pool forks configured in `package.json` (`test:unit`).
  - Code Contracts Runner: `tests/run-tests.mjs` running 17 modular contract test files.

#### 2.2 Backend Component (`tourvaa-admin-backend`)
- **Framework**: FastAPI 0.115.0 / Starlette 0.38.6 / Pydantic v2
- **Language / Runtime**: Python 3.12.10
- **Process Manager**: `uvicorn.exe` running `app.main:app --reload` on port 8000
- **Active Base URL**: `http://127.0.0.1:8000/api`
- **Documentation Endpoints**:
  - Swagger UI: `http://127.0.0.1:8000/docs` (HTTP 200 Verified)
  - OpenAPI Specification: `http://127.0.0.1:8000/openapi.json` (785 operations)
  - Health Check Endpoint: `http://127.0.0.1:8000/api/health` (HTTP 200 Verified)
- **Environment Mode**: `APP_ENV = development`, `APP_DEBUG = true`
- **Test Automation**:
  - Pytest: Configured in `pytest.ini` with `addopts = --basetemp=.pytest_tmp`, `pythonpath = .`
  - Test Suite: 110 test files containing 864 test functions in `tests/`.

#### 2.3 Database Engine (`tourvaa_db_demo`)
- **RDBMS**: MySQL Community Server version 8.0.46
- **Connection URL**: `mysql+pymysql://root:***@localhost:3306/tourvaa_db_demo`
- **ORM / Migrations**: SQLAlchemy 2.0 with Alembic (170 migration versions)
- **Database Metrics**:
  - Total Database Tables: **139 tables** (138 domain models + 1 `alembic_version`)
  - Total Foreign Key Constraints: **252 Foreign Keys**
  - Active Connection Status: Verified operational with < 10ms round-trip latency.

---

### 3. Safety & Boundary Assessment

| Environmental Check | Observed State | Risk Assessment | Mitigation / Safety Rule |
| :--- | :--- | :--- | :--- |
| **Database Environment** | Local MySQL database `tourvaa_db_demo` contains sample demo seed data (34 users, 9 tours, 35 bookings). | Low Risk | No write/delete operations executed against production databases. Read-only queries executed for integrity audit. |
| **Payment Gateways** | Stripe (`pk_...`), PayPal sandbox configured in `.env`. | Moderate Risk | Tests avoid initiating live captures. Financial tests executed against pure unit calculations or sandbox mocks. |
| **Notification Services** | Real SMTP server configured (`mail.ayatiworks.com:465`). | High Risk | Notification tests restricted to serialization units (`test_notification_delivery_unit.py`) preventing live email dispatch. |
| **External Tour APIs** | Viator API configured in sandbox mode (`VIATOR_ENV = sandbox`). | Low Risk | Tests evaluate local model transformations without issuing paid third-party bookings. |
| **Redis Cache** | `REDIS_URL` is empty in `.env`. | Low Risk | System operates with in-memory fallbacks for session and rate-limit tracking. |

---

### 4. Environmental Gaps & Limitations

1. **Redis Service Inactive**: The Redis cache service is not running on port 6379. While the application gracefully falls back to in-memory dictionaries for rate limiting and WebSocket connection tracking, this prevents testing multi-worker Redis cluster synchronization.
2. **Pytest Cache Directory Permissions**: Running pytest generated a `PytestCacheWarning` due to Windows file permission restrictions on `.pytest_cache/v/cache`. This was mitigated using the `--basetemp=.pytest_tmp` switch.
3. **OpenAPI JSON Payload Latency**: Because the OpenAPI schema encompasses 785 route operations across 61 tags, full dynamic serialization via `/openapi.json` takes > 3.5 seconds on first request, requiring increased client timeouts during automated probes.
