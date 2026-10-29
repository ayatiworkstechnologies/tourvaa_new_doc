# Production Deployment Architecture & Infrastructure Topology

This document details the production container topology, networking, storage persistence, reverse proxy integration, and CI/CD automation of the Tourvaa platform.

---

## 1. Production Deployment Topology Diagram

```mermaid
flowchart TD
    subgraph INTERNET["Public Internet"]
        USERS["Visitors, Customers & Partners"]
        ADMINS["Tourvaa Staff & Administrators"]
        WEBHOOKS["Stripe & PayPal Webhook Events"]
    end

    subgraph CLOUD_EDGE["Edge & Ingress (Cloudflare / Reverse Proxy)"]
        EDGE_ROUTER["Reverse Proxy / SSL Ingress (Nginx / Traefik / Cloudflare)<br/>TLS 1.3 Termination | Strict HTTP Security Headers"]
    end

    subgraph DOCKER_HOST["Production Container Host (Docker / Container Cluster)"]
        subgraph FRONTEND_CONTAINER["Frontend Service (tourvaa-admin-frontend)"]
            NODE_SERVER["Node.js 22 Standalone Server (server.js)<br/>Port 3000 | Non-Root user: nextjs<br/>Healthcheck: fetch('http://127.0.0.1:3000/')"]
        end

        subgraph BACKEND_CONTAINER["Backend Service (tourvaa-admin-backend)"]
            ENTRYPOINT["docker-entrypoint.sh<br/>Alembic upgrade head (retries 30x)"]
            UVICORN_PROC["Uvicorn ASGI Server (app.main:app)<br/>Port 8000 | Non-Root user: tourvaa<br/>Healthcheck: GET /api/health"]
            ENTRYPOINT --> UVICORN_PROC
        end

        subgraph PERSISTENCE_CONTAINERS["Persistence Services"]
            MYSQL_SRV[("MySQL 8.0+ Database Server<br/>Port 3306 | InnoDB Engine<br/>Volume: mysql_data")]
            REDIS_SRV[("Redis Server (redis:8.0)<br/>Port 6379 | Appendonly: yes<br/>Volume: redis_data")]
        end

        subgraph VOLUMES["Host Mounted Volumes"]
            STOR_VOL[("Host Volume: /data/storage<br/>Public asset uploads")]
            PRIV_VOL[("Host Volume: /data/private-docs<br/>Invoices, Receipts, Partner KYC")]
        end
    end

    subgraph EXTERNAL_SERVICES["External Cloud Infrastructure"]
        CLOUDINARY_CDN["Cloudinary Media CDN<br/>(Image optimization & public storage)"]
        SMTP_RELAY["SMTP Mail Relay<br/>(SendGrid / Google Workspace / Postmark)"]
        STRIPE_API["Stripe API & Webhook Services"]
        PAYPAL_API["PayPal Sandbox & Live REST API"]
    end

    %% Inbound connections
    USERS -->|HTTPS :443| EDGE_ROUTER
    ADMINS -->|HTTPS :443| EDGE_ROUTER
    WEBHOOKS -->|HTTPS :443| EDGE_ROUTER

    %% Edge to containers
    EDGE_ROUTER -->|HTTP :3000 (Storefront & Portals)| NODE_SERVER
    EDGE_ROUTER -->|WSS :8000 (/api/ws/messages)| UVICORN_PROC
    EDGE_ROUTER -->|HTTP :8000 (Webhook Endpoints)| UVICORN_PROC

    %% Container to container
    NODE_SERVER -->|Internal HTTP Proxy (/api/*)| UVICORN_PROC
    UVICORN_PROC -->|TCP :3306 (SQLAlchemy)| MYSQL_SRV
    UVICORN_PROC -->|TCP :6379 (Locks & WS)| REDIS_SRV
    UVICORN_PROC -->|Filesystem Mount| STOR_VOL
    UVICORN_PROC -->|Filesystem Mount| PRIV_VOL

    %% Backend to external
    UVICORN_PROC -->|REST API| CLOUDINARY_CDN
    UVICORN_PROC -->|SMTP TLS :465| SMTP_RELAY
    UVICORN_PROC -->|HTTPS API| STRIPE_API
    UVICORN_PROC -->|HTTPS API| PAYPAL_API
```

---

## 2. Infrastructure & Container Components

### 2.1 Edge Ingress & Reverse Proxy
- **TLS Termination**: All incoming traffic arrives on port 443 with modern TLS (TLS 1.2/1.3).
- **Reverse Proxy Routing**:
  - `/*` routes forward to the Next.js frontend container on `http://frontend:3000`.
  - `/api/ws/messages` WebSocket upgrade requests are routed directly to the backend on `http://backend:8000`.
  - Direct webhook paths (`/api/payments/stripe/webhook`, `/api/payments/paypal/webhook`) can be routed directly to the backend to minimize hop latency.

### 2.2 Frontend Container (`tourvaa-admin-frontend`)
- **Base Image**: `node:22-alpine`.
- **Runtime User**: Runs as unprivileged user `nextjs:nodejs` (UID/GID 1001).
- **Standalone Build**: Leverages Next.js `output: "standalone"`, packing only necessary dependencies into `server.js` and reducing container size from ~1.2GB to <180MB.
- **Healthcheck**: Periodically polls `http://127.0.0.1:3000/` every 30 seconds.

### 2.3 Backend Container (`tourvaa-admin-backend`)
- **Base Image**: `python:3.12-slim`.
- **System Dependencies**: Includes `libgomp1` (required by ONNX runtime for FastEmbed embeddings).
- **Runtime User**: Runs as unprivileged user `tourvaa:tourvaa` (UID/GID 1001).
- **Entrypoint Script (`docker-entrypoint.sh`)**:
  - Checks `RUN_MIGRATIONS=true`.
  - Executes `python -m alembic upgrade head` with up to 30 retries, guaranteeing the database schema is up-to-date before Uvicorn starts.
- **Healthcheck**: Queries `http://127.0.0.1:8000/api/health` every 30 seconds.

### 2.4 Data Persistence Volumes
- **MySQL Volume (`/var/lib/mysql`)**: Ensures durable database records survive container updates.
- **Redis Volume (`/data`)**: Configured with `appendonly yes` for persistent distributed lock keys and rate-limit tracking.
- **Storage Volume (`/data/storage`)**: Houses static asset uploads served via `/storage`.
- **Private Docs Volume (`/data/private-docs`)**: Stores generated PDF invoices, itineraries, booking receipts, and partner business documents outside the public web root.
