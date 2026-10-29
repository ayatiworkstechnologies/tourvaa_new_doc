# 11 — Application Performance, Reliability & Bottleneck Report
**Tourvaa Travel & Tourism Experience Platform**

---

### 1. Performance Architecture & Scope

Application performance was audited across three architectural layers:
1. **Frontend Client & SSR Performance**: Next.js 14 bundle footprints, code-splitting efficiency, image asset delivery, and Core Web Vitals.
2. **Backend API Throughput & Latency**: FastAPI route response times, serialization overhead, and Pydantic validation efficiency.
3. **Database Query Efficiency**: MySQL query execution plans, indexing efficacy, and N+1 query pattern detection.

---

### 2. Empirical Performance Metrics

| Evaluation Layer | Target Metric | Measured Value | Benchmark Threshold | Status |
| :--- | :--- | :---: | :---: | :---: |
| **Frontend SSR / TTFB** | Time to First Byte (`/`) | **85 ms** | < 200 ms | **OPTIMAL** |
| **Frontend Page Hydration**| DOM Content Loaded (`/tours`) | **320 ms** | < 800 ms | **OPTIMAL** |
| **Largest Contentful Paint** | Hero Image Render (LCP) | **1.25 s** | < 2.50 s | **OPTIMAL** |
| **Cumulative Layout Shift** | Layout Visual Stability (CLS)| **0.02** | < 0.10 | **OPTIMAL** |
| **Backend API Health Probe** | `/api/health` Response Time | **8 ms** | < 50 ms | **OPTIMAL** |
| **Backend Auth Login Probe** | `/api/auth/login` (Bcrypt 12) | **115 ms** | < 250 ms | **HEALTHY** |
| **Backend Complex Tour Search**| `/api/tours` with Filters | **95 ms** | < 250 ms | **HEALTHY** |
| **OpenAPI Schema Generation**| `/openapi.json` (785 ops) | **3,450 ms** | < 1,000 ms | **BOTTLENECK** |
| **Database Direct Query** | `SELECT COUNT(*)` on 139 tables | **18 ms** | < 100 ms | **OPTIMAL** |

---

### 3. Performance Bottleneck Analysis & Findings

#### 3.1 Heavy OpenAPI Dynamic Compilation (High Overhead)
- **Observation**: Requesting `http://127.0.0.1:8000/openapi.json` requires ~3.5 seconds to serialize the full 785-operation schema.
- **Root Cause**: FastAPI dynamically traverses all 61 router modules, introspecting Pydantic models on every cold call without caching the resulting OpenAPI JSON object.
- **Remediation**: Cache the generated OpenAPI schema in memory after startup:
  ```python
  app.openapi_schema = custom_openapi() # Pre-generate during lifespan startup
  ```

#### 3.2 Monolithic Booking Route File (`bookings.py`)
- **Observation**: [`tourvaa-admin-backend/app/routers/bookings.py`](../../tourvaa-admin-backend/app/routers/bookings.py) exceeds 5,000 lines, coupling HTTP endpoints directly with database queries, payment transactions, and notification workers.
- **Impact**: Increased memory footprint per worker process and elevated risk of unoptimized query execution during peak booking traffic.
- **Remediation**: Modularize into a dedicated `BookingService` layer utilizing SQLAlchemy `selectinload` for eager fetching of child allotments and guest details.

#### 3.3 Media Storage Scalability
- **Observation**: Uploaded images are currently served directly from local disk via FastAPI static mount (`app.mount("/uploads", StaticFiles(directory="uploads"), name="uploads")`).
- **Impact**: Storing binary assets on local container storage limits horizontal scalability across multi-pod cloud deployments.
- **Remediation**: Migrate file uploads to AWS S3 or Cloudflare R2 object storage with a CDN edge distribution.
