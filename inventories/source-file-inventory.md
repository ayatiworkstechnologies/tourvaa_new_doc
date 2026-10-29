# Project Source File Inventory

This document catalogs the principal source code files, configurations, migrations, and test suites across the Tourvaa platform.

---

## 1. Workspace Repositories Overview

| Repository Directory | Technology Stack | Purpose / Scope |
|---|---|---|
| [`tourvaa-admin-backend/`](../../tourvaa-admin-backend) | Python 3.12, FastAPI 0.139.2 (baseline 0.115), SQLAlchemy 2.0.51, Alembic, MySQL | REST API server, WebSocket server, authentication, background workers, PDF generation, AI RAG engine. |
| [`tourvaa-admin-frontend/`](../../tourvaa-admin-frontend) | Node 22, Next.js 16.4.3 (baseline 15.5), React 19.2.4, TypeScript 5, Tailwind CSS 4 | Public customer storefront, Admin console, Supplier portal, Agent portal, Affiliate portal, Customer portal. |

---

## 2. Backend Architecture Inventory (`tourvaa-admin-backend`)

### 2.1 Core App Entry & Configuration

| File Path | Description & Responsibility | Key Classes / Functions |
|---|---|---|
| [`app/main.py`](../../tourvaa-admin-backend/app/main.py) | Application entrypoint, lifespan startup/shutdown, middleware mounting, background task worker loops, healthcheck. | `FastAPI()`, `_lifespan()`, `validate_production_config()`, `start_background_jobs()`, `health()` |
| [`app/config/__init__.py`](../../tourvaa-admin-backend/app/config/__init__.py) | Pydantic Settings model loading environment variables, domain secret resolvers, CORS parsing, production guard rules. | `Settings()`, `get_auth_secret()`, `get_portal_secret()`, `get_storage_root()` |
| [`app/database/__init__.py`](../../tourvaa-admin-backend/app/database/__init__.py) | SQLAlchemy engine initialization, session factory (`SessionLocal`), declarative Base, DB dependency `get_db()`. | `engine`, `SessionLocal`, `Base`, `get_db()` |
| [`app/seed.py`](../../tourvaa-admin-backend/app/seed.py) | Database seeder for roles, permissions, modules, admin accounts, reference data. | `seed_default_roles_and_permissions()`, `seed_reference_data()` |
| [`docker-entrypoint.sh`](../../tourvaa-admin-backend/docker-entrypoint.sh) | Container entrypoint running migrations before starting Uvicorn worker process. | Shell migration loop with retry, `exec uvicorn` |
| [`Dockerfile`](../../tourvaa-admin-backend/Dockerfile) | Multi-stage production container build (Python 3.12-slim, non-root `tourvaa` user, volume mounts). | Docker stages `builder` and `runtime` |

### 2.2 Security & Authentication (`app/auth/`)

| File Path | Description & Responsibility | Key Classes / Functions |
|---|---|---|
| [`app/auth/security.py`](../../tourvaa-admin-backend/app/auth/security.py) | Password hashing via Bcrypt, dual-domain JWT creation & decoding, portal-to-domain mapping. | `hash_password()`, `verify_password()`, `create_token()`, `decode_auth_token()` |
| [`app/auth/permissions.py`](../../tourvaa-admin-backend/app/auth/permissions.py) | FastAPI dependency injection for current authenticated user, token validation, RBAC permission checker, approval guards. | `get_current_user()`, `require_permission()`, `expand_permission_slugs()` |

### 2.3 Middleware (`app/middleware/`)

| File Path | Description & Responsibility | Key Functions |
|---|---|---|
| [`app/middleware/cors.py`](../../tourvaa-admin-backend/app/middleware/cors.py) | Configures CORSMiddleware with credentials support and production origin enforcement. | `setup_cors(app)` |
| [`app/middleware/api_cache.py`](../../tourvaa-admin-backend/app/middleware/api_cache.py) | Adds `Cache-Control: no-store` headers to all API responses to prevent client/proxy caching of private data. | `ApiNoStoreMiddleware` |
| [`app/middleware/csrf.py`](../../tourvaa-admin-backend/app/middleware/csrf.py) | Validates Origin/Referer headers for state-changing HTTP requests. | `CsrfMiddleware` |
| [`app/middleware/error_handlers.py`](../../tourvaa-admin-backend/app/middleware/error_handlers.py) | Global exception handlers for standard JSON error formatting. | `register_error_handlers(app)` |

### 2.4 Routers (`app/routers/` - 51 Files)

| Key Router Files | Prefixes / Endpoints | Primary Responsibility |
|---|---|---|
| [`app/routers/auth.py`](../../tourvaa-admin-backend/app/routers/auth.py) | `/api/auth/*` | Login, registration, token refresh, logout, password resets, 2FA setup. |
| [`app/routers/tours.py`](../../tourvaa-admin-backend/app/routers/tours.py) | `/api/tours/*` | Tour catalog CRUD, itineraries, inclusions, pricing, departures, media. |
| [`app/routers/bookings.py`](../../tourvaa-admin-backend/app/routers/bookings.py) | `/api/bookings/*` | Booking creation, status transitions, supplier assignment, communications. |
| [`app/routers/payments.py`](../../tourvaa-admin-backend/app/routers/payments.py) | `/api/payments/*` | Payment records, authorizations, captures, manual transactions. |
| [`app/routers/payments_gateway.py`](../../tourvaa-admin-backend/app/routers/payments_gateway.py) | `/api/payments/*` | Stripe Checkout sessions, PayPal orders, webhooks, refund processing. |
| [`app/routers/invoices.py`](../../tourvaa-admin-backend/app/routers/invoices.py) | `/api/invoices/*` | Invoice generation, balance due tracking, PDF downloads. |
| [`app/routers/suppliers.py`](../../tourvaa-admin-backend/app/routers/suppliers.py) | `/api/suppliers/*` | Supplier onboarding, vehicle details, bank accounts, profile verification. |
| [`app/routers/supplier_ledger.py`](../../tourvaa-admin-backend/app/routers/supplier_ledger.py) | `/api/supplier-ledger/*` | Supplier earnings ledger, payout requests, bank details. |
| [`app/routers/agents.py`](../../tourvaa-admin-backend/app/routers/agents.py) | `/api/agents/*` | Agent business verification, markup settings, B2B customer management. |
| [`app/routers/agent_ledger.py`](../../tourvaa-admin-backend/app/routers/agent_ledger.py) | `/api/agent-ledger/*` | Agent commission tracking, commercial statements, payout reconciliation. |
| [`app/routers/affiliates.py`](../../tourvaa-admin-backend/app/routers/affiliates.py) | `/api/affiliates/*` | Affiliate profile, marketing info, verification review. |
| [`app/routers/affiliate_tracking.py`](../../tourvaa-admin-backend/app/routers/affiliate_tracking.py) | `/api/affiliate/*` | Affiliate link management, click tracking, conversion stats, wallet. |
| [`app/routers/messaging.py`](../../tourvaa-admin-backend/app/routers/messaging.py) | `/api/messaging/*`, `/api/ws/*` | Thread messaging, WebSocket ticket generation, realtime socket stream. |
| [`app/routers/notifications.py`](../../tourvaa-admin-backend/app/routers/notifications.py) | `/api/notifications/*` | In-app notifications, mark-read, WebPush subscription registration. |
| [`app/routers/chatbot.py`](../../tourvaa-admin-backend/app/routers/chatbot.py) | `/api/chatbot/*` | Public chat session, message inference, FAQ management, feedback. |
| [`app/routers/cms.py`](../../tourvaa-admin-backend/app/routers/cms.py) | `/api/cms/*` | Categories, subcategories, countries, cities, policy terms. |
| [`app/routers/website_cms.py`](../../tourvaa-admin-backend/app/routers/website_cms.py) | `/api/website-cms/*` | Homepage banners, blogs, popular destinations, customer reviews. |
| [`app/routers/public.py`](../../tourvaa-admin-backend/app/routers/public.py) | `/api/public/*` | Unauthenticated tour search, destination pages, blogs, reviews, leads. |
| [`app/routers/reports.py`](../../tourvaa-admin-backend/app/routers/reports.py) | `/api/reports/*` | Sales, financial, operational reports, CSV/Excel export, report schedules. |
| [`app/routers/settings.py`](../../tourvaa-admin-backend/app/routers/settings.py) | `/api/settings/*` | Platform app settings, API settings, currency master, SMTP settings. |

### 2.5 Services Layer (`app/services/` - 56 Files)

| Key Service Files | Primary Responsibility |
|---|---|
| [`app/services/bookings.py`](../../tourvaa-admin-backend/app/services/bookings.py) | Core booking state machine, deposit calculation, seat allocation, expiry loop. |
| [`app/services/payments.py`](../../tourvaa-admin-backend/app/services/payments.py) | Payment authorization lifecycle, manual transactions, hold release sweeps. |
| [`app/services/payments_gateway.py`](../../tourvaa-admin-backend/app/services/payments_gateway.py) | Stripe and PayPal gateway API communication and webhook verification. |
| [`app/services/invoices.py`](../../tourvaa-admin-backend/app/services/invoices.py) | PDF invoice creation via ReportLab, balance reminder sweeps. |
| [`app/services/cancellations.py`](../../tourvaa-admin-backend/app/services/cancellations.py) | Cancellation refund policy evaluation, gateway refund execution. |
| [`app/services/messaging_ws.py`](../../tourvaa-admin-backend/app/services/messaging_ws.py) | WebSocket connection registry, ticket store, Redis pub/sub relay. |
| [`app/services/notification_delivery.py`](../../tourvaa-admin-backend/app/services/notification_delivery.py) | Durable email delivery queue with retry logic and template rendering. |
| [`app/services/notifications_push.py`](../../tourvaa-admin-backend/app/services/notifications_push.py) | WebPush delivery via `pywebpush` using VAPID keys. |
| [`app/services/rag.py`](../../tourvaa-admin-backend/app/services/rag.py) & [`embeddings.py`](../../tourvaa-admin-backend/app/services/embeddings.py) | Vector embeddings using fastembed and cosine similarity ranking. |
| [`app/services/viator.py`](../../tourvaa-admin-backend/app/services/viator.py) | External Day Tours proxy connecting to Viator Partner API. |
| [`app/services/retention.py`](../../tourvaa-admin-backend/app/services/retention.py) | Scheduled daily data pruning for sessions, logs, and expired records. |

---

## 3. Frontend Architecture Inventory (`tourvaa-admin-frontend`)

### 3.1 Routing & App Shell (`src/app/` - 163 Pages)

| Route Group | Primary Pages | Layout / Guard Structure |
|---|---|---|
| `%28public%29/` | `/`, `/tours`, `/tours/[id]`, `/destinations/[slug]`, `/blogs/[slug]`, `/cart`, `/booking/[id]`, `/about`, `/contact` | `PublicLayout`, SEO metadata injectors, PublicSettingsProvider |
| `admin/` | `/admin/dashboard`, `/admin/tours`, `/admin/bookings`, `/admin/payments`, `/admin/users`, `/admin/settings`, `/admin/cms`, `/admin/reports` | `AdminLayout`, `AdminRouteGuard`, role permissions checker |
| `customer/` | `/customer/dashboard`, `/customer/bookings`, `/customer/invoices`, `/customer/travellers`, `/customer/wishlist`, `/customer/profile` | `CustomerPortalLayout`, `ProtectedRoute` (customer) |
| `supplier/` | `/supplier/dashboard`, `/supplier/tours`, `/supplier/bookings`, `/supplier/earnings`, `/supplier/payouts`, `/supplier/profile` | `SupplierPortalLayout`, `ProtectedRoute` (supplier) |
| `agent/` | `/agent/dashboard`, `/agent/tours`, `/agent/bookings`, `/agent/invoices`, `/agent/payouts`, `/agent/customers` | `AgentPortalLayout`, `ProtectedRoute` (agent) |
| `affiliate/` | `/affiliate/dashboard`, `/affiliate/referral-links`, `/affiliate/clicks`, `/affiliate/conversions`, `/affiliate/wallet` | `AffiliatePortalLayout`, `ProtectedRoute` (affiliate) |

### 3.2 Security & Proxy

| File Path | Description |
|---|---|
| [`src/proxy.ts`](../../tourvaa-admin-frontend/src/proxy.ts) | Next.js 16 server-side proxy middleware enforcing session cookie presence on protected prefixes and normalizing URLs. |
| [`next.config.ts`](../../tourvaa-admin-frontend/next.config.ts) | Next.js build configuration, API/storage rewrites, CSP headers, allowed dev origins. |

### 3.3 State & API Providers (`src/providers/` & `src/lib/api/`)

| File Path | Description |
|---|---|
| [`src/providers/AuthProvider.tsx`](../../tourvaa-admin-frontend/src/providers/AuthProvider.tsx) | React Context managing user authentication state, current user profile, and logout triggers. |
| [`src/providers/PublicSettingsProvider.tsx`](../../tourvaa-admin-frontend/src/providers/PublicSettingsProvider.tsx) | Context providing public platform settings, active currencies, and branding config. |
| [`src/providers/TravelStoreProvider.tsx`](../../tourvaa-admin-frontend/src/providers/TravelStoreProvider.tsx) | Context managing cart, wishlist, booking draft state, and guest session details. |
| [`src/lib/api/client.ts`](../../tourvaa-admin-frontend/src/lib/api/client.ts) | Axios HTTP client configured with credentials, base URL, and interceptors for 401 handling. |
| [`src/lib/api/publicClient.ts`](../../tourvaa-admin-frontend/src/lib/api/publicClient.ts) | Axios client for unauthenticated public storefront requests. |

---

## 4. Quality Assurance & Test Suites

| Location | Test Count / Type | Scope |
|---|---|---|
| [`tourvaa-admin-backend/tests/`](../../tourvaa-admin-backend/tests) | 111 test files (Pytest) | Unit tests, RBAC matrices, payment workflows, booking lifecycle, migrations. |
| [`tourvaa-admin-frontend/tests/unit/`](../../tourvaa-admin-frontend/tests/unit) | 18 test files (Vitest) | React component tests, custom hooks, currency conversion, tour validation. |
| [`tourvaa-admin-frontend/tests/*.test.mjs`](../../tourvaa-admin-frontend/tests) | 15 Node.js test runners | Contract verification, responsive UI checks, flow validations. |
| [`tourvaa-admin-frontend/e2e/`](../../tourvaa-admin-frontend/e2e) | 8 test suites (Playwright) | Critical user flows, admin console audits, supplier and agent console audits. |
