# 01 — Project Overview & Executive Summary

## 1. Executive Summary

**Tourvaa** is an enterprise-grade multi-role travel booking, tour catalog, and partner marketplace platform developed by Ayatiworks. The platform facilitates end-to-end travel lifecycle management—from public tour discovery, personalized itinerary customization, and secure multi-currency booking checkout, to supplier acceptance, operational dispatch, B2B wholesale agent reservations, and affiliate marketing referral tracking.

The system is engineered as a decoupled modern web application comprising an asynchronous Python 3.12 / FastAPI backend API and a Next.js 16 / React 19 frontend supporting seven distinct user personas across dedicated portal interfaces.

---

## 2. Core Business Value Propositions

1. **Multi-Role Marketplace Ecosystem**: Unified governance for 7 distinct user roles: Super Administrator, Administrator, Sub-Administrator, Tour Supplier / Operator, B2B Travel Agent / Reseller, Marketing Affiliate, and Public Customer / Traveller.
2. **Defensive Booking & Payment Escrow Architecture**: Payment success is intentionally decoupled from final booking confirmation. Customer funds are held via pre-authorization holds on Stripe/PayPal during a 4-day supplier acceptance window before capture.
3. **Comprehensive Tour Catalog Engine**: Multi-day tour builder with day-by-day itineraries, room categories, pricing tiers (adult, child, infant, single supplement), departure calendars with seat quotas, and automated discount campaigns.
4. **Partner Financial Ledgers**: Automated double-entry balance sheets for suppliers (net tour earnings minus platform commission) and travel agents (commission earnings and client markup settlements) with withdrawal payout workflows.
5. **Integrated Marketing & Growth Channels**: Native affiliate referral tracking with short links (`/r/{code}`), 30-day attribution windows, custom commission rules, and wallet payouts.
6. **Local AI Customer Support (RAG)**: Self-hosted retrieval-augmented generation assistant running FastEmbed / ONNX (`BAAI/bge-small-en-v1.5`) on CPU without recurring third-party LLM costs.
7. **External Inventory Integration**: Seamless integration with the Viator Partner API to offer local day trips and experiences alongside proprietary multi-day itineraries.

---

## 3. User Roles & Access Architecture

| Role Name | Slug | Portal Interface | Primary Business Functions & Access Scope |
|---|---|---|---|
| **Super Administrator** | `super-admin` | `/admin/*` | Unrestricted platform governance, system configuration, database seeding, staff user management, payment gateway keys. |
| **Administrator** | `admin` | `/admin/*` | Daily back-office operations: tour approval reviews, booking management, manual payment captures, refund processing, CMS content. |
| **Sub-Administrator** | `sub-admin` | `/admin/*` | Operational staff role with scoped module permissions (e.g. customer support messaging, enquiry management, email log inspection). |
| **Tour Supplier / Operator** | `supplier` | `/supplier/*` | Tour creation, departures calendar management, booking request acceptance/rejection, vehicle KYC registration, earnings ledger, payout requests. |
| **B2B Agent / Reseller** | `agent-reseller`| `/agent/*` | Wholesale catalog access, reserving bookings on behalf of retail clients, custom client markup management, commercial ledger statements. |
| **Marketing Affiliate** | `affiliate` | `/affiliate/*` | Creation of trackable referral short links, real-time click and conversion analytics, commission earnings tracking, wallet payout requests. |
| **Customer / Traveller** | `customer` | `/customer/*` | Tour discovery, wishlist tracking, checkout payment, saved family traveller manifests, booking receipts, cancellation requests, support chat. |

---

## 4. Repository Structure & Workspace Organization

The platform is maintained within a single monorepo workspace containing two primary service directories:

- [`tourvaa-admin-backend/`](../tourvaa-admin-backend): Asynchronous FastAPI REST & WebSocket application, SQLAlchemy ORM models, Alembic migrations, background worker coroutines, PDF document generation, and RAG vector search.
- [`tourvaa-admin-frontend/`](../tourvaa-admin-frontend): Next.js 16 App Router application hosting the public consumer storefront and the role-based management consoles for Admin, Supplier, Agent, Affiliate, and Customer portals.
