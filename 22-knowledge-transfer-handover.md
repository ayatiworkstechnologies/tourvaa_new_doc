# 22 — Client Technical Handover & Operational Runbook

## 1. Handover Overview

This document formalizes the technical handover of the Tourvaa travel platform from Ayatiworks Technologies to Tourvaa platform operators.

---

## 2. Production Service Inventory

| Service Component | Host / Runtime | Primary Configuration | Operational Responsibility |
|---|---|---|---|
| **API Backend** | Docker Container | `tourvaa-admin-backend` on port 8000 | FastAPI REST & WebSocket endpoints, background workers. |
| **Web Frontend** | Docker Container / Vercel | `tourvaa-admin-frontend` on port 3000 | Next.js SSR storefront and multi-role partner portals. |
| **Relational Database**| Managed MySQL 8.0+ | Port 3306 (InnoDB) | Master persistence for all 138 tables. Daily automated backups required. |
| **In-Memory Cache**| Managed Redis 8.0+ | Port 6379 | Distributed sweep locks, rate-limiting, WebSocket message pub/sub. |
| **Document Storage**| Persistent File Volume | `/data/private-docs` | Immutable booking confirmation receipts, invoices, partner KYC. |

---

## 3. Essential Administrative Credentials & Key Contacts

- **Super Administrator Account**: Created during initial database seeding via `SUPER_ADMIN_EMAIL` and `SUPER_ADMIN_PASSWORD`.
- **Payment Gateways**: Credentials managed via encrypted database table `payment_settings` via `/admin/settings/payment`.
- **Engineering Escalation**: Ayatiworks Technologies — Lead Architect Rubankumar Sankar.
