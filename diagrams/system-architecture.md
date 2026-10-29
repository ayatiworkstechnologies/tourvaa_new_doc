# System Architecture Diagram & Walkthrough

This document illustrates the end-to-end system architecture of the Tourvaa travel platform, showing the multi-tier boundaries between users, frontend edge layers, backend API services, asynchronous workers, persistence layers, and external service providers.

---

## 1. High-Level Architecture Diagram

```mermaid
flowchart TB
    subgraph CLIENTS["Client Access Tier"]
        BROWSER["Web Browser / Mobile Client<br/>(Desktop, Tablet, Mobile)"]
    end

    subgraph EDGE["Edge & Routing Tier (Next.js 16)"]
        PROXY["Next.js Proxy (src/proxy.ts)<br/>Cookie Verification & Route Shield"]
        REWRITE["Next.js Route Proxy (next.config.ts)<br/>Rewrites /api and /storage"]
        SSR["Server Component Rendering<br/>(React 19 / Next.js)"]
        SPA["Client-Side Portals (SPA)<br/>Admin / Supplier / Agent / Affiliate / Customer"]
    end

    subgraph API_TIER["FastAPI Application Tier (Port 8000)"]
        UVICORN["Uvicorn ASGI Server<br/>(Multi-Worker Concurrency)"]
        MIDDLEWARE["Middleware Stack<br/>(CORS, ApiNoStore, CSRF, ErrorHandlers)"]
        ROUTERS["API Routers (51 Modular Routers)<br/>(/api/* and /r/*)"]
        AUTH_GUARD["Authentication & RBAC<br/>(Dual JWT Domain & RolePermission Checker)"]
        SERVICES["Domain Services Layer (56 Services)<br/>(Bookings, Payments, Tours, Ledgers, etc.)"]
        WS_HANDLER["WebSocket Hub (/api/ws/messages)<br/>(Realtime Messaging & Live Notifications)"]
    end

    subgraph BACKGROUND["Background Workers & Scheduled Sweeps"]
        STALE_SWEEP["Stale Booking Expiry (15m)<br/>Releases Unpaid Calendar Seats"]
        HOLD_SWEEP["Payment Hold Release (60m)<br/>Releases Expired Gateway Authorizations"]
        CAPTURE_SWEEP["Payment Capture Retry (15m)<br/>Retries Accepted Booking Captures"]
        EMAIL_RETRY["Lifecycle Email Retry (15m)<br/>Exponential Backoff 1m/5m/25m"]
        REMINDERS["Booking & Balance Reminders (60m)<br/>Automated Traveller & Agent Alerts"]
        RETENTION["Data Retention Pruning (24h)<br/>Prunes Old Sessions & Chat Logs"]
    end

    subgraph STORAGE["Persistence & Data Tier"]
        MYSQL[("MySQL 8.0+ Database<br/>(InnoDB Engine, 138 Tables)")]
        REDIS[("Redis Cache & Pub/Sub<br/>(Distributed Lock & WS Relay)")]
        LOCAL_DISK[("Private Disk Storage<br/>(private-docs: Invoices, Itineraries, Docs)")]
    end

    subgraph EXTERNAL["External Third-Party Services"]
        STRIPE["Stripe Payment Gateway<br/>(Manual Capture & Webhooks)"]
        PAYPAL["PayPal REST API<br/>(Authorize & Capture Orders)"]
        CLOUDINARY["Cloudinary Media CDN<br/>(Public Tour & CMS Images)"]
        VIATOR["Viator Partner API<br/>(External Day Trips & Experiences)"]
        SMTP["SMTP Mail Server<br/>(Lifecycle & Transactional Emails)"]
        WEBPUSH["WebPush Push Services<br/>(FCM / Mozilla VAPID)"]
        GEOIP["GeoIP Provider (ip-api / ipapi)<br/>(Currency & Locale Auto-Detection)"]
    end

    %% Client flows
    BROWSER -->|HTTPS Requests| PROXY
    BROWSER -->|Direct WebSocket Upgrade (wss://)| UVICORN

    %% Edge flows
    PROXY --> SSR
    PROXY --> SPA
    SSR --> REWRITE
    SPA --> REWRITE
    REWRITE -->|HTTP Forwarding| UVICORN

    %% API Tier flows
    UVICORN --> MIDDLEWARE
    MIDDLEWARE --> ROUTERS
    ROUTERS --> AUTH_GUARD
    AUTH_GUARD --> SERVICES
    ROUTERS --> WS_HANDLER

    %% Persistence flows
    SERVICES -->|SQLAlchemy 2.0 Pool| MYSQL
    SERVICES -->|Distributed Locks & Keys| REDIS
    SERVICES -->|Direct FS Read/Write| LOCAL_DISK
    WS_HANDLER -->|Pub/Sub Channel ws:messages| REDIS

    %% Background worker flows
    BACKGROUND -->|acquire_sweep_lock| REDIS
    BACKGROUND -->|Scheduled Task Execution| SERVICES

    %% External integration flows
    SERVICES -->|REST API & Webhooks| STRIPE
    SERVICES -->|REST API & Webhooks| PAYPAL
    SERVICES -->|Asset Uploads| CLOUDINARY
    SERVICES -->|Partner API Requests| VIATOR
    SERVICES -->|SMTP TLS Connection| SMTP
    SERVICES -->|VAPID HTTP/2 Push| WEBPUSH
    SERVICES -->|REST Query| GEOIP
```

---

## 2. Component Descriptions & Boundaries

### 2.1 Client Access Tier
Users connect via standard modern web browsers on desktop, tablet, and mobile devices. All public web traffic terminates at the Next.js edge router over HTTPS. WebSocket connections upgrade directly to the backend origin (`NEXT_PUBLIC_WS_URL`) over secure WebSockets (`wss://`).

### 2.2 Edge & Routing Tier (Next.js 16)
- **`src/proxy.ts`**: Implements Next.js 16's server-side proxy convention (formerly middleware). Checks for the presence of the `tourvaa_access` session cookie on all protected portal routes (`/admin/*`, `/customer/*`, `/supplier/*`, `/agent/*`, `/affiliate/*`) before serving React Server Components, preventing HTML flashes of unauthorized UI.
- **`next.config.ts`**: Provides path rewriting that transparently proxies client browser calls to `/api/:path*` and `/storage/:path*` directly to `API_PROXY_TARGET`. It also enforces HTTP Content Security Policy (CSP), frame guards, and client max body size limits (`60mb` for video uploads).

### 2.3 FastAPI Application Tier
- **Uvicorn Server**: Production ASGI server configured with single or multiple workers. Supports process-level concurrency and HTTP/1.1 and WebSocket protocols.
- **Middleware Pipeline**:
  - `setup_cors`: Strictly enforces permitted origins from `ALLOWED_ORIGINS` with credentials enabled.
  - `ApiNoStoreMiddleware`: Appends `Cache-Control: no-store` headers to eliminate stale caching of dynamic user data.
  - `CsrfMiddleware`: Defends state-modifying requests (`POST`, `PUT`, `DELETE`, `PATCH`).
  - `register_error_handlers`: Normalizes uncaught exceptions and HTTP validation errors into unified JSON error structures.
- **Dual-Domain Authentication**: Authenticates JWTs using segregated signing keys for administration staff (`admin` domain) vs external portal users (`normal` domain).
- **Service Layer**: Houses 56 dedicated business domain services that decouple database queries and external APIs from the router handlers.

### 2.4 Background Scheduler
FastAPI lifespan background task loops run concurrently without external worker dependencies (like Celery), leveraging `app/utils/distributed_lock.py` backed by Redis:
- Stale unpaid booking seat release (15-minute sweep)
- Payment hold release after 4-day decision window (60-minute sweep)
- Payment capture retry following supplier acceptance (15-minute sweep)
- Durable email delivery retry with exponential backoff (15-minute sweep)
- Customer balance-due reminders and travel date notifications (60-minute sweep)
- Data retention pruning for sessions and chat messages (24-hour sweep)

### 2.5 Data & Storage Tier
- **MySQL 8.0+ Database**: Stores the relational schema across 138 tables with InnoDB ACID guarantees.
- **Redis Cache**: Backs distributed locking (`acquire_sweep_lock`), rate-limiting buckets, WebSocket single-use ticket store, and cross-worker pub/sub messaging.
- **Private Disk Storage**: Dedicated filesystem root (`private-docs/`) segregated from public static storage, holding confidential documents (supplier business licenses, agent agreements, generated invoices, and booking receipts).

### 2.6 External Integrations
Provides modular connectivity to Stripe (holds & captures), PayPal (orders & authorizations), Cloudinary (CDN media), Viator (third-party day tours), SMTP (transactional mail), WebPush (browser push notifications), and GeoIP (browsing currency localization).
