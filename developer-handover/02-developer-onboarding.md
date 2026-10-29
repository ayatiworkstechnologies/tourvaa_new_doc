# Chapter 02: New Developer Onboarding Guide

## 1. Onboarding Checklist (Day 1 to Day 3)

| Timeline | Milestone Goal | Key Deliverable |
|---|---|---|
| **Day 1** | Local Environment Bootstrapped | Backend & Frontend dev servers running locally on `localhost:8000` and `localhost:3000`. |
| **Day 2** | Database & Test Suites Verified | All 110 backend Pytest suites and 41 frontend unit tests passing without errors. |
| **Day 3** | End-to-End Workflow Walkthrough | Complete a local test booking from public search through payment confirmation. |

---

## 2. Required Software & Runtime Prerequisites

Ensure the following tools are installed on your workstation:
1. **Git**: Version `2.40+`
2. **Node.js**: Version `20.x LTS` (Node 18.x also supported)
3. **Python**: Version `3.12.x` (Do not use Python 3.13 due to C-extension dependencies in ONNX)
4. **MySQL Community Server**: Version `8.0.x`
5. **Redis Server** (Optional for local dev; required if running multiple Uvicorn workers)
6. **Recommended IDE**: Visual Studio Code with Python, Pylance, Tailwind CSS, and ESLint extensions

---

## 3. Repository Cloning & Directory Layout

The Tourvaa workspace is organized as follows:
```
d:/ayatiworks/2026/tourvaa/
├── tourvaa-admin-backend/         # FastAPI backend service
├── tourvaa-admin-frontend/        # Next.js 14 App Router frontend
└── technical-documentation/       # Complete architectural documentation & handover guides
```

Clone the repository and enter the workspace:
```bash
git clone <repository_url> tourvaa
cd tourvaa
```

---

## 4. Key Developer Responsibilities

Incoming engineers must adhere to the following code governance rules:
- **Zero Hallucination Rule**: Never commit unverified assumptions about payment gateways or third-party APIs.
- **Safety Rule**: Never modify production database schemas directly; always write explicit Alembic migrations.
- **CSRF & Auth Compliance**: All mutating frontend requests must route through `api` client to attach `X-CSRF-Token`.
