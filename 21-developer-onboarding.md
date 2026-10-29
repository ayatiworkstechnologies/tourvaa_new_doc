# 21 — Developer Onboarding Guide

Welcome to the Tourvaa engineering team! This guide outlines your 30-day onboarding curriculum.

---

## 1. Day 1 to Day 3: Environment Setup & Architecture
- Complete local setup following [`14-local-development-setup.md`](14-local-development-setup.md).
- Review [System Architecture](diagrams/system-architecture.md) and [Database ERD](diagrams/database-erd.md).
- Run test suites in both repositories (`pytest tests` and `npm run test:unit`).

## 2. Week 1: Understanding Core Booking & Payment Escrow
- Read [Booking Lifecycle Workflow](diagrams/booking-lifecycle-flow.md).
- Inspect [`app/services/bookings.py`](../tourvaa-admin-backend/app/services/bookings.py) and [`app/services/payments.py`](../tourvaa-admin-backend/app/services/payments.py).
- Practice creating a tour as a supplier, submitting it for admin approval, and booking it as a customer.

## 3. Week 2: Partner Portals & Financial Ledgers
- Explore the Supplier Portal (`/supplier/*`), Agent Portal (`/agent/*`), and Affiliate Portal (`/affiliate/*`).
- Understand how net supplier earnings and agent markups are calculated in `supplier_ledger.py` and `agent_ledger.py`.

## 4. Month 1: Production Maintenance & Feature Development
- Review CI/CD pipelines in `.github/workflows/ci-cd.yml`.
- Understand background task scheduling and distributed locking in `app/utils/distributed_lock.py`.
