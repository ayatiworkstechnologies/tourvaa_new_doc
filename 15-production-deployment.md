# 15 — Production Deployment & CI/CD Pipeline

## 1. Container Build Strategy

Both applications utilize multi-stage Docker builds to maximize security and minimize container footprints.

### Backend Container (`tourvaa-admin-backend/Dockerfile`)
- Stage 1 (`builder`): Compiles dependencies into `/install`.
- Stage 2 (`runtime`): `python:3.12-slim` containing only runtime packages, `libgomp1` for ONNX, and non-root user `tourvaa:tourvaa` (UID 1001).
- Entrypoint (`docker-entrypoint.sh`): Executes `python -m alembic upgrade head` with up to 30 retries before launching Uvicorn.

### Frontend Container (`tourvaa-admin-frontend/Dockerfile`)
- Stage 1 (`dependencies`): `npm ci` caching.
- Stage 2 (`builder`): `node:22-alpine` running `npm run build` with `NEXT_OUTPUT_STANDALONE=true`.
- Stage 3 (`runtime`): Copies `.next/standalone`, public assets, and `.next/static`. Runs as unprivileged `nextjs` user.

---

## 2. GitHub Actions CI/CD Pipeline

1. **Backend CI (`.github/workflows/ci-cd.yml`)**:
   - Spawns disposable MySQL 8.4 service container.
   - Executes `alembic upgrade head` and `alembic check` (verifies models have migrations).
   - Seeds deterministic CI fixtures (`python -m scripts.seed_ci_fixtures`).
   - Runs full Pytest test suite (`python -m pytest -q`).
   - Builds candidate Docker image and performs **Trivy vulnerability scan** (failing on critical/high CVEs).
   - Publishes image to GitHub Container Registry (`ghcr.io`).

2. **Frontend CI (`.github/workflows/ci-cd.yml`)**:
   - Checks out sibling backend repo for API contract verification.
   - Runs ESLint (`npm run lint`), Vitest unit tests (`npm run test:unit`), and TypeScript checks (`tsc --noEmit`).
   - Runs cross-repo contract verification (`node tests/run-tests.mjs`).
   - Builds standalone Next.js bundle and runs Playwright smoke regressions.
   - Scans and publishes production container image.
