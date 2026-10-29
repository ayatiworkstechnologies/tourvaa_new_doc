# Environment Variables Inventory & Reference

This document provides a comprehensive, verified catalog of all environment variables used by the Tourvaa travel platform across the FastAPI backend and Next.js frontend.

---

## 1. Backend Environment Variables (`tourvaa-admin-backend`)

The backend configuration is managed via Pydantic Settings in [`app/config/__init__.py`](../../tourvaa-admin-backend/app/config/__init__.py) and loaded from `.env`.

### 1.1 Application Core & Environment

| Variable | Type | Default Value | Production Requirement | Purpose & Description |
|---|---|---|---|---|
| `APP_NAME` | `str` | `"Tourvaa Backend"` | Optional | Human-readable title for the application and OpenAPI schema. |
| `APP_ENV` | `str` | `"production"` | **Required** | Environment identifier (`development`, `staging`, `production`). **Fails closed** to `"production"` if unset. |
| `APP_DEBUG` | `bool` | `False` | **Must be `False`** | FastAPI debug mode. Refuses to start in production if set to `True`. |
| `DATABASE_URL` | `str` | *None* | **Required** | SQLAlchemy database connection string, e.g. `mysql+pymysql://user:pass@host:3306/tourvaa_db`. |
| `PORT` | `int` | `8000` | Optional | Port for Uvicorn to bind to. Read by `docker-entrypoint.sh` and Dockerfile. |
| `WEB_CONCURRENCY` | `int` | `1` | Optional | Number of Uvicorn workers. If `> 1`, `REDIS_URL` **must** be provided. |
| `RUN_MIGRATIONS` | `bool` | `True` | Optional | Used in `docker-entrypoint.sh` to auto-execute `alembic upgrade head` before process start. |
| `MIGRATION_MAX_ATTEMPTS` | `int` | `30` | Optional | Maximum retry attempts waiting for MySQL container readiness during container boot. |
| `FORWARDED_ALLOW_IPS` | `str` | `"127.0.0.1"` | Optional | Reverse proxy IPs trusted for `X-Forwarded-For` / `X-Forwarded-Proto` forwarding. |

### 1.2 Authentication & JWT Security

| Variable | Type | Default Value | Production Requirement | Purpose & Description |
|---|---|---|---|---|
| `JWT_SECRET_KEY` | `str` | *None* | **Required** | Fallback secret key for HMAC-SHA256 JWT signing. |
| `ADMIN_JWT_SECRET_KEY` | `str` | `""` | **Required (>=32 chars)** | Dedicated signing key for administrative roles (`super-admin`, `admin`, `sub-admin`). Must differ from `NORMAL_JWT_SECRET_KEY`. |
| `NORMAL_JWT_SECRET_KEY` | `str` | `""` | **Required (>=32 chars)** | Dedicated signing key for external portal roles (`customer`, `supplier`, `agent`, `affiliate`). |
| `JWT_ALGORITHM` | `str` | `"HS256"` | Optional | Cryptographic algorithm for JWT signatures. |
| `ACCESS_TOKEN_EXPIRE_MINUTES` | `int` | `1440` (24h) | Optional | Lifetime of bearer/cookie access tokens. |
| `REFRESH_TOKEN_EXPIRE_DAYS` | `int` | `30` | Optional | Lifetime of refresh tokens tracked in `user_sessions`. |
| `SETTINGS_ENCRYPTION_KEY` | `str` | `""` | **Required (64 hex chars)** | 256-bit AES encryption key used to encrypt payment credentials and API keys in the DB. **Never rotate after launch**. |

### 1.3 User Account Security & Rate Limiting

| Variable | Type | Default Value | Production Requirement | Purpose & Description |
|---|---|---|---|---|
| `REQUIRE_EMAIL_VERIFICATION` | `bool` | `False` | Recommended (`True`) | Enforces email verification via token link before new accounts can authenticate. |
| `EMAIL_VERIFICATION_EXPIRE_MINUTES` | `int` | `1440` | Optional | Expiry duration for email verification tokens. |
| `OTP_EXPIRE_MINUTES` | `int` | `10` | Optional | Expiry duration for OTP codes sent via email. |
| `OTP_MAX_ATTEMPTS` | `int` | `5` | Optional | Maximum invalid attempts before OTP code invalidation. |
| `LOGIN_MAX_FAILED_ATTEMPTS` | `int` | `5` | Optional | Threshold of consecutive password failures before triggering temporary account lockout. |
| `LOGIN_LOCKOUT_MINUTES` | `int` | `15` | Optional | Duration an account remains locked after exceeding max failed attempts. |
| `TRUST_PROXY_HEADERS` | `bool` | `False` | Condition-dependent | If `True`, trusts `X-Forwarded-For` for IP rate limiting. Only enable behind trusted reverse proxies. |
| `MOBILE_DEEP_LINK_URL` | `str` | `"tourvaa://reset-password"` | Optional | Deep-link scheme used for mobile app password reset redirects. |

### 1.4 Web & CORS Networking

| Variable | Type | Default Value | Production Requirement | Purpose & Description |
|---|---|---|---|---|
| `FRONTEND_URL` | `str` | `"http://localhost:3000"` (dev) / `"https://tourvaa.vercel.app"` (prod) | **Required** | Base URL of the frontend application for email links, redirects, and password resets. |
| `API_BASE_URL` | `str` | `"http://127.0.0.1:8000"` | Optional | Base URL of the API server used for generating webhook callbacks and affiliate redirects. |
| `ALLOWED_ORIGINS` | `str` | `"*"` (dev only) | **Explicit comma-separated list** | Allowed CORS origins. **Wildcard `*` is strictly refused in production** to protect credentialed cookies. |

### 1.5 Seed & Bootstrap Admin Accounts

| Variable | Type | Default Value | Production Requirement | Purpose & Description |
|---|---|---|---|---|
| `SUPER_ADMIN_NAME` | `str` | `"Super Admin"` | Optional | Name of bootstrap super-admin account. |
| `SUPER_ADMIN_EMAIL` | `str` | `"admin@tourvaa.com"` | **Must be configured** | Email of bootstrap super-admin. |
| `SUPER_ADMIN_PASSWORD` | `str` | `"Tourvaa@2026!"` | **Must change from default** | Initial password. Validated at startup to refuse default passwords in production. |
| `SUPER_ADMIN_RESET_PASSWORD_ON_STARTUP` | `bool` | `False` | Optional | If `True`, resets password to configured value on server restart. |
| `ADMIN_NAME` / `ADMIN_EMAIL` / `ADMIN_PASSWORD` | - | `"Admin"` / `"admin.user@tourvaa.com"` / `"Tourvaa@2026!"` | **Configure in production** | Bootstrap administrative user credentials. |
| `SUB_ADMIN_NAME` / `SUB_ADMIN_EMAIL` / `SUB_ADMIN_PASSWORD` | - | `"Sub Admin"` / `"subadmin@tourvaa.com"` / `"Tourvaa@2026!"` | **Configure in production** | Bootstrap sub-administrative user credentials. |

### 1.6 Storage & Cloudinary

| Variable | Type | Default Value | Production Requirement | Purpose & Description |
|---|---|---|---|---|
| `STORAGE_ROOT` | `str` | `"storage"` | Optional | Directory path for local file storage (relative to backend root or absolute). |
| `CLOUDINARY_URL` | `str` | `""` | Optional | Format: `cloudinary://API_KEY:API_SECRET@CLOUD_NAME`. Enables Cloudinary CDN for public tour & CMS assets. |
| `CLOUDINARY_PUBLIC_ROOT` | `str` | `"tourvaa_demo/public"` | Optional | Folder namespace in Cloudinary for public media assets. |

### 1.7 SMTP Email Delivery

| Variable | Type | Default Value | Production Requirement | Purpose & Description |
|---|---|---|---|---|
| `SMTP_HOST` | `str \| None` | `None` | **Required for emails** | SMTP server hostname (e.g. `smtp.sendgrid.net`, `smtp.gmail.com`). |
| `SMTP_PORT` | `int` | `465` | Optional | Port for SMTP (465 for SSL, 587 for STARTTLS). |
| `SMTP_USERNAME` / `SMTP_USER` | `str \| None` | `None` | **Required for emails** | SMTP authentication username. |
| `SMTP_PASSWORD` | `str \| None` | `None` | **Required for emails** | SMTP authentication password / API key. |
| `SMTP_FROM_NAME` | `str` | `"Tourvaa"` | Optional | Sender display name. |
| `SMTP_FROM_EMAIL` | `str \| None` | `None` | **Required for emails** | Sender email address (`no-reply@tourvaa.com`). |
| `SMTP_REPLY_TO` | `str \| None` | `None` | Optional | Reply-To address (`support@tourvaa.com`). |
| `SMTP_USE_SSL` | `bool` | `True` | Optional | Enable direct SSL encryption (Port 465). |
| `SMTP_STARTTLS` | `bool` | `False` | Optional | Enable STARTTLS encryption (Port 587). |
| `SMTP_TIMEOUT_SECONDS` | `int` | `20` | Optional | Socket timeout for SMTP connections. |

### 1.8 Payment Gateways (Stripe & PayPal)

| Variable | Type | Default Value | Production Requirement | Purpose & Description |
|---|---|---|---|---|
| `STRIPE_PUBLISHABLE_KEY` | `str` | `""` | Optional | Seeded into database `payment_settings` for Stripe client integration. |
| `STRIPE_SECRET_KEY` | `str` | `""` | Optional | Seeded into database `payment_settings` for Stripe API calls. |
| `STRIPE_WEBHOOK_SECRET` | `str` | `""` | **Required in production** | Webhook signing secret (`whsec_...`) used to verify Stripe signatures. Refuses startup if missing. |
| `PAYPAL_CLIENT_ID` | `str` | `""` | Optional | Seeded into database `payment_settings` for PayPal OAuth. |
| `PAYPAL_CLIENT_SECRET` | `str` | `""` | Optional | Seeded into database `payment_settings` for PayPal OAuth. |
| `PAYPAL_MODE` | `str` | `"sandbox"` | Optional | `"sandbox"` or `"live"`. Determines API host (`api-m.sandbox.paypal.com` vs `api-m.paypal.com`). |
| `PAYPAL_WEBHOOK_ID` | `str` | `""` | **Required in production** | PayPal Webhook ID from developer portal for webhook signature verification. Refuses startup if missing. |

### 1.9 Redis & Distributed Concurrency

| Variable | Type | Default Value | Production Requirement | Purpose & Description |
|---|---|---|---|---|
| `REDIS_URL` | `str` | `""` | **Required if WEB_CONCURRENCY > 1** | Redis connection URI (`redis://:password@host:6379/0`). Backs distributed sweep locks, rate limits, and WebSocket pub/sub. |

### 1.10 Viator Partner API (Day Tours & Experiences)

| Variable | Type | Default Value | Production Requirement | Purpose & Description |
|---|---|---|---|---|
| `VIATOR_API_KEY` | `str` | `""` | Optional | Fallback partner API key. Primary key is managed in admin settings. |
| `VIATOR_AFFILIATE_PID` / `VIATOR_PID` | `str` | `""` | Optional | Partner ID (P + 8 digits) for commission attribution. |
| `VIATOR_ENV` | `str` | `"sandbox"` | Optional | `"sandbox"` or `"production"`. Sets API gateway destination. |
| `VIATOR_API_BASE_URL` | `str` | `""` | Optional | Custom endpoint override. |
| `VIATOR_ENABLED` | `bool` | `True` | Optional | Global deployment switch for external tours. |
| `VIATOR_CAMPAIGN_PREFIX` | `str` | `"tourvaa"` | Optional | Tracking campaign tag prefix for outbound affiliate links. |
| `VIATOR_TIMEOUT_SECONDS` | `float` | `15.0` | Optional | HTTP request timeout. |

### 1.11 WebPush Notifications (VAPID)

| Variable | Type | Default Value | Production Requirement | Purpose & Description |
|---|---|---|---|---|
| `VAPID_PUBLIC_KEY` | `str` | `""` | Optional | Base64URL-encoded VAPID public key sent to browsers for push subscriptions. |
| `VAPID_PRIVATE_KEY_FILE` | `str` | `"vapid_private.pem"` | Optional | Path to local PEM file containing VAPID private key. |
| `VAPID_PRIVATE_KEY` | `str` | `""` | Optional | Raw PEM string or base64url private key (convenient alternative to file). |
| `VAPID_MAILTO` | `str` | `"mailto:admin@tourvaa.com"` | Optional | Contact email included in JWT headers sent to push services (FCM/Mozilla). |

### 1.12 AI Chatbot & GeoIP

| Variable | Type | Default Value | Production Requirement | Purpose & Description |
|---|---|---|---|---|
| `CHATBOT_EMBEDDING_MODEL` | `str` | `"BAAI/bge-small-en-v1.5"` | Optional | Local ONNX model name downloaded on first run via `fastembed` for RAG semantic search. |
| `GEOIP_PROVIDER` | `str` | `"ip-api"` | Optional | GeoIP provider (`ip-api` or `ipapi`) for browsing currency detection. |
| `GEOIP_API_KEY` | `str` | `""` | Optional | License key for commercial GeoIP lookups. |
| `DEFAULT_CURRENCY` | `str` | `"USD"` | Optional | Fallback display currency. |
| `DEFAULT_LOCALE` | `str` | `"en-US"` | Optional | Fallback locale string. |

---

## 2. Frontend Environment Variables (`tourvaa-admin-frontend`)

Frontend variables are read at build time and runtime in Next.js.

| Variable | Build / Runtime | Default Value | Production Requirement | Purpose & Description |
|---|---|---|---|---|
| `API_PROXY_TARGET` | **Build & Runtime** | `"http://127.0.0.1:8000"` | **Required** | Destination host for Next.js `/api/:path*` and `/storage/:path*` rewrites. Refuses production build if unset. |
| `NEXT_PUBLIC_WS_URL` | **Build & Runtime** | Derived from `API_PROXY_TARGET` | **Required (wss://)** | WebSocket endpoint baked into the client bundle for `/api/ws/messages` connections. **Must use `wss://` in production**. |
| `NEXT_PUBLIC_SITE_URL` | **Build & Runtime** | `"http://localhost:3000"` | **Required** | Canonical website URL used for generating OpenGraph, Twitter card, sitemap, and SEO tags. |
| `NEXT_OUTPUT_STANDALONE` | **Build** | *None* | Set to `true` in Docker | Directs Next.js to compile a minimal standalone Node.js server bundle for Docker containers. |
| `BUILD_ENV` | **Build** | `"development"` | Set to `production` in CI/CD | Validates that `API_PROXY_TARGET`, `NEXT_PUBLIC_WS_URL`, and `NEXT_PUBLIC_SITE_URL` are not localhost/defaults. |
| `TOURVAA_TEST_PYTHON` | **Test** | *Auto-detected* | Optional | Path to backend Python virtualenv for running cross-repo contract tests. |

---

## 3. Production Validation Gates

The application implements rigorous, fail-safe environment validation checks:

1. **`validate_production_config()`** (in backend [`app/main.py`](../../tourvaa-admin-backend/app/main.py)):
   - Checks `APP_DEBUG == False`
   - Verifies `SUPER_ADMIN_PASSWORD != "Admin@123"`
   - Verifies `ADMIN_JWT_SECRET_KEY` length >= 32 characters
   - Verifies `NORMAL_JWT_SECRET_KEY` length >= 32 characters
   - Verifies `ADMIN_JWT_SECRET_KEY != NORMAL_JWT_SECRET_KEY`
   - Checks `STRIPE_WEBHOOK_SECRET` is non-empty
   - Checks `PAYPAL_WEBHOOK_ID` is non-empty
   - Fails immediately with `RuntimeError` if any check fails.

2. **`validate_worker_concurrency()`** (in backend [`app/main.py`](../../tourvaa-admin-backend/app/main.py)):
   - Rejects `WEB_CONCURRENCY > 1` if `REDIS_URL` is empty.

3. **`validate_database_migration_head()`** (in backend [`app/main.py`](../../tourvaa-admin-backend/app/main.py)):
   - Compares the running database migration head against the code migration head and aborts startup on drift.

4. **Frontend Docker Build Gate** (in frontend [`Dockerfile`](../../tourvaa-admin-frontend/Dockerfile)):
   - If `BUILD_ENV=production`, aborts build if `API_PROXY_TARGET`, `NEXT_PUBLIC_WS_URL`, or `NEXT_PUBLIC_SITE_URL` contain `localhost` or `127.0.0.1`.
