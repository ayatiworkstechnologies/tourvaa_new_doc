# Developer Knowledge Transfer (KT) & Technical Handover Portal

## Welcome to the Tourvaa Engineering Handover

This dedicated portal serves as the authoritative, production-grade Knowledge Transfer (KT) package for incoming Principal Architects, Full-Stack Engineers, Database Administrators, DevOps Engineers, and QA Leads taking ownership of the Tourvaa travel and experience platform.

---

## Handover Package Navigation Structure

```
developer-handover/
├── README.md                                # Master portal index & navigation (this document)
├── 01-project-handover-overview.md          # High-level architecture, technology stack, and verified components
├── 02-developer-onboarding.md               # Step-by-step Day-1 onboarding & environment prerequisites
├── 03-local-setup-guide.md                  # Comprehensive local development setup (Backend, Frontend, DB)
├── 04-frontend-knowledge-transfer.md        # Next.js App Router, components, route guards, and state management
├── 05-backend-knowledge-transfer.md         # FastAPI routers, service layer, dependency injection, and schemas
├── 06-database-knowledge-transfer.md        # 139-table schema, Alembic migrations, constraints, and backup runbook
├── 07-module-handover.md                    # Deep-dive breakdown of all 20 business modules and workflows
├── 08-authentication-authorization.md       # Dual-domain JWT cookies, 2FA TOTP, RBAC matrix, and permission checks
├── 09-api-integration-guide.md              # Frontend-to-backend Axios client, interceptors, and endpoint mapping
├── 10-deployment-server-handover.md         # Dockerfiles, Uvicorn concurrency, Nginx proxies, and deployment flows
├── 11-troubleshooting-guide.md              # 16 concrete operational incident playbooks and diagnostics
├── 12-how-to-extend-project.md              # Step-by-step recipes for adding pages, APIs, models, and migrations
├── 13-testing-regression-checklist.md       # 25 Backend tests & 17 frontend test suites, E2E flows, and QA checklist
├── 14-known-issues-pending-work.md          # Master technical debt and gap register (P0 to P3 tracking)
├── 15-maintenance-guide.md                  # Database maintenance, log rotation, secret rotation, and upgrades
├── 16-production-support-runbook.md         # L1/L2/L3 support procedures, health monitoring, and on-call runbook
├── 17-handover-checklist.md                 # Formal sign-off and verification checklist for handover completion
└── diagrams/                                # Dedicated architecture and sequence diagrams
    ├── system-overview.md                   # Full-stack system topology and traffic ingress
    ├── frontend-backend-flow.md             # Client-to-API communication and interceptor sequence
    ├── database-erd.md                      # Core entity relational architecture and joins
    ├── authentication-sequence.md           # Login, JWT issuance, and refresh token lifecycle
    ├── deployment-flow.md                   # Containerization, migration, and rolling release flow
    └── module-workflows.md                  # End-to-end booking, payment, and supplier state machines
```

---

## Handover Verification Standard

Every instruction, command, file path, and architectural assertion in this handover package has been verified against the physical codebase of [`tourvaa-admin-backend`](../../tourvaa-admin-backend) and [`tourvaa-admin-frontend`](../../tourvaa-admin-frontend).
