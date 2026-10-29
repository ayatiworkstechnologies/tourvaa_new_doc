# 04 — Project File & Directory Structure

This document details the complete hierarchical layout of the Tourvaa project workspace.

```text
d:/ayatiworks/2026/tourvaa/
├── tourvaa-admin-backend/                  # FastAPI Application Repository
│   ├── alembic/                           # Database Migration Management
│   │   ├── versions/                      # 170 Migration Script Files (2026-06 to 2026-10)
│   │   └── env.py                         # Alembic Runtime Configuration & Model Imports
│   ├── app/                               # Core Python Application Package
│   │   ├── api/                           # API Routing Aggregation
│   │   │   └── router.py                  # Master Router Registration & Route Grouping
│   │   ├── auth/                          # Security, JWT, and RBAC Dependencies
│   │   │   ├── permissions.py             # User Injection, Role & Approval Guards
│   │   │   └── security.py                # Bcrypt Hashing & Dual-Domain JWT Tokens
│   │   ├── config/                        # Settings Management
│   │   │   └── __init__.py                # Pydantic Settings & Startup Production Validations
│   │   ├── database/                      # Database Initialization & Session Factory
│   │   │   └── __init__.py                # SQLAlchemy Engine, SessionLocal, Base
│   │   ├── integrations/                  # Third-Party External API Clients
│   │   │   ├── external_tours/            # Generic External Tour Contracts
│   │   │   └── viator/                    # Viator Partner API Client, Schemas & Mapper
│   │   ├── middleware/                    # HTTP Request / Response Middlewares
│   │   │   ├── api_cache.py               # ApiNoStoreMiddleware (no-store headers)
│   │   │   ├── cors.py                    # CORS Origins & Credentials Setup
│   │   │   ├── csrf.py                    # CSRF Origin & Referer Verification
│   │   │   └── error_handlers.py          # Unified JSON Exception Handlers
│   │   ├── models/                        # 33 SQLAlchemy Model Modules (138 DB Tables)
│   │   ├── routers/                       # 51 API Routers Implementing Endpoints
│   │   ├── schemas/                       # Pydantic v2 Request & Response DTO Schemas
│   │   ├── services/                      # 56 Business Domain Services
│   │   └── utils/                         # Shared Utilities (Money, PDF, Mailer, Locks)
│   ├── scripts/                           # Administrative & Seed Scripts
│   ├── tests/                             # 111 Pytest Test Suite Files
│   ├── Dockerfile                         # Production Multi-Stage Dockerfile (Python 3.12-slim)
│   ├── docker-entrypoint.sh               # Migration Loop & Uvicorn Launch Script
│   ├── requirements.txt                   # Production Python Dependencies
│   └── alembic.ini                        # Alembic Configuration File
│
├── tourvaa-admin-frontend/                 # Next.js 16 Application Repository
│   ├── e2e/                               # 8 Playwright E2E Test Suite Files
│   ├── public/                            # Static Web Assets, Icons, and Logos
│   ├── src/                               # Application Source Code
│   │   ├── app/                           # Next.js App Router (163 Page Routes)
│   │   │   ├── %28public%29/                  # Public Storefront & Marketing Pages
│   │   │   ├── admin/                     # Administrative Management Console
│   │   │   ├── customer/                  # Customer / Traveller Portal
│   │   │   ├── supplier/                  # Tour Operator / Supplier Portal
│   │   │   ├── agent/                     # B2B Travel Agent / Reseller Portal
│   │   │   ├── affiliate/                 # Marketing Affiliate Portal
│   │   │   ├── layout.tsx                 # Root Layout (Typography & Providers)
│   │   │   └── not-found.tsx              # 404 Error Page
│   │   ├── components/                    # 21 Subdirectories of Reusable UI Components
│   │   ├── hooks/                         # 16 Custom React Hooks
│   │   ├── lib/                           # Frontend Libraries, API Services, Utilities
│   │   │   ├── api/                       # Axios Client Instances & Domain Services
│   │   │   ├── constants/                 # Booking Status, Themes, Navigation Links
│   │   │   ├── seo/                       # Metadata Generators & Structured JSON-LD
│   │   │   └── utils/                     # Currency, Date, Validation Utilities
│   │   ├── providers/                     # React Context Providers (Auth, Settings, Store)
│   │   └── proxy.ts                       # Next.js 16 Edge Proxy (Session Cookie Guard)
│   ├── tests/                             # 18 Vitest Unit Tests & 15 Node Contract Tests
│   ├── Dockerfile                         # Standalone Next.js Production Dockerfile (Node 22)
│   ├── next.config.ts                     # Next.js Config, CSP Headers & API Rewrites
│   ├── package.json                       # Node Dependencies & Build Scripts
│   └── tsconfig.json                      # TypeScript Configuration
│
└── technical-documentation/               # Complete Project Technical Knowledge Base
    ├── README.md                          # Documentation Master Index & Navigation Homepage
    ├── modules/                           # 20 Individual Module Markdown Files
    ├── diagrams/                          # 11 Dedicated Mermaid Architecture Diagrams
    └── inventories/                       # 6 Exhaustive CSV/Markdown Reference Inventories
```

The complete inventory of all key source files and their responsibilities is cataloged in [`inventories/source-file-inventory.md`](inventories/source-file-inventory.md).
