# Chapter 13 — Final Technical Handover & Developer Onboarding

## 1. Handover Overview & Target Audience

This technical handover guide is prepared for incoming engineering leads, full-stack developers, and DevOps maintainers responsible for operating, scaling, and maintaining the Tourvaa platform.

---

## 2. Core Repository Structure

```
d:/ayatiworks/2026/tourvaa/
├── tourvaa-admin-backend/         # FastAPI 0.139.2 Backend API (baseline 0.115)
│   ├── app/
│   │   ├── api/                   # central registry: 50 source modules / 64 mounted router instances
│   │   ├── auth/                  # JWT security, cookies, and RBAC permissions
│   │   ├── config/                # Environment settings & validation
│   │   ├── database/              # SQLAlchemy session generator & seeds
│   │   ├── middleware/            # CSRF, CORS, and cache-control middleware
│   │   ├── models/                # documented inventory: 138 ORM application tables
│   │   ├── schemas/               # Pydantic v2 validation models
│   │   ├── services/              # Business logic (payments, messaging, retention)
│   │   └── utils/                 # Distributed lock, currency, encryption
│   ├── alembic/                   # Database migrations (118 versions)
│   ├── tests/                     # Pytest automated test suites
│   ├── Dockerfile                 # Multi-stage production container
│   └── docker-entrypoint.sh       # Migration runner and Uvicorn process manager
│
├── tourvaa-admin-frontend/        # Next.js 16.4.3 App Router Frontend (baseline 15.5)
│   ├── src/
│   │   ├── app/                   # 163 Next.js pages across all portals
│   │   ├── components/            # Reusable UI, modals, tables, and headers
│   │   ├── hooks/                 # Shared React hooks (auth, currency, compare)
│   │   ├── lib/
│   │   │   ├── api/               # Axios client, session tokens, service callers
│   │   │   ├── seo/               # Dynamic metadata generator (pageMetadata)
│   │   │   └── utils/             # Formatters, dashboard redirects, dates
│   ├── tests/                     # 17 Node.js contract test suites
│   ├── Dockerfile                 # Standalone production container
│   └── next.config.ts             # Rewrites, CSP headers, and image optimization
│
└── technical-documentation/       # Comprehensive 50+ document architecture suite
```

---

## 3. Developer Quickstart Guide

### Backend Local Setup
```bash
cd tourvaa-admin-backend
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
pip install -r requirements-dev.txt

# Configure local environment
cp .env.example .env

# Run database migrations
python -m alembic upgrade head

# Start local API server
python -m uvicorn app.main:app --reload --port 8000
```

### Frontend Local Setup
```bash
cd tourvaa-admin-frontend
npm ci
cp .env.example .env.local

# Run contract tests
node tests/run-tests.mjs

# Start Next.js development server
npm run dev
```

---

## 4. Key Operational Tasks

- **Seeding Database**: `python -m app.database.seed` creates initial roles, permissions, and super-admin accounts.
- **Running Automated Tests**:
  - Backend: `pytest -v`
  - Frontend: `node tests/run-tests.mjs` and `npm run test:unit`
  - Static Type Check: `npx tsc --noEmit`
- **Inspecting Background Tasks**: Background tasks in `app/main.py` output structured log entries prefixed with task identifiers (e.g. `[expire_stale_bookings]`, `[payment_hold]`).
