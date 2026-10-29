# Chapter 03 — Frontend Production Readiness

## 1. Architecture & App Router Evaluation

The frontend application (`tourvaa-admin-frontend`) is constructed on **Next.js 16.4.3** (locked in `package.json`; upgraded from initial 15.5 baseline) utilizing the App Router architecture, React 19.2.4, and TailwindCSS.

### Production Build & Compilation Status
- **Type Checking**: Clean execution of `npx tsc --noEmit` across all 163 pages with **0 errors**.
- **Page Tree Completeness**: Exactly 163 page entry points across public, admin, customer, agent, supplier, and affiliate portals.
- **SEO & Layout Coverage**: 100% of routes export standard OpenGraph and title metadata via `metadataFor()`, following the addition of [src/app/admin/invoice-templates/layout.tsx](../../tourvaa-admin-frontend/src/app/admin/invoice-templates/layout.tsx).

---

## 2. Build-Time Environment Variable Compilation

In Next.js standalone container builds ([Dockerfile](../../tourvaa-admin-frontend/Dockerfile)), three critical environment variables are compiled into static assets and reverse proxy rewrites:

```dockerfile
ARG API_PROXY_TARGET=http://backend:8000
ARG NEXT_PUBLIC_WS_URL=ws://localhost:8000
ARG NEXT_PUBLIC_SITE_URL=http://localhost:3000
```

### Production Release Requirement:
When building production Docker images (`BUILD_ENV=production`), the pipeline enforces that these variables must point to real production hostnames rather than local defaults:
- `API_PROXY_TARGET`: Internal Kubernetes/Docker backend service URL (e.g. `http://tourvaa-backend:8000`).
- `NEXT_PUBLIC_WS_URL`: Public WebSocket endpoint (e.g. `wss://api.tourvaa.com`).
- `NEXT_PUBLIC_SITE_URL`: Public canonical domain (e.g. `https://www.tourvaa.com`).

Failure to supply these build arguments at build time will trigger an explicit assertion failure in `Dockerfile` line 44, preventing misconfigured images from reaching production.

---

## 3. UI/UX & Responsive Behavior

The 17 automated contract suites in `tests/run-tests.mjs` validated:
1. **Viewport Boundaries**: Modals ([ActionModal.tsx](../../tourvaa-admin-frontend/src/components/operations/ActionModal.tsx), [ConfirmDialog.tsx](../../tourvaa-admin-frontend/src/components/ui/ConfirmDialog.tsx), [BookingPaymentModal.tsx](../../tourvaa-admin-frontend/src/components/bookings/BookingPaymentModal.tsx)) stay inside mobile viewports without vertical clipping.
2. **Table Responsiveness**: All wide data tables support horizontal overflow scrolling with fixed headers.
3. **Motion Preferences**: Hero animations respect `prefers-reduced-motion` settings.
4. **Header Layouts**: Language widget lanes and role-specific navigation render cleanly across 375px mobile, 768px tablet, and 1280px+ desktop resolutions.
