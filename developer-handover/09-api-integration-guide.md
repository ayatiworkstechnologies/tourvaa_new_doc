# Chapter 09: API Integration & Frontend-to-Backend Guide

## 1. Axios Client & Request Lifecycle

Frontend API communication is centralized in [`src/lib/api/client.ts`](../../tourvaa-admin-frontend/src/lib/api/client.ts).

### Request Interceptor
Automatically reads the `tourvaa_csrf` cookie and injects the `X-CSRF-Token` header for all mutating HTTP requests (POST, PUT, DELETE, PATCH).

### Response Interceptor
Intercepts `401 Unauthorized` responses. Triggers an automatic token refresh call to `POST /api/auth/refresh-token`. If refresh succeeds, the failed original request is retried seamlessly. If refresh fails, auth state is cleared and user is redirected to `/login`.

---

## 2. Frontend-to-Backend API Mapping

| Frontend Page | Purpose / Function | Target API Endpoint | Backend Router | Service File | Database Tables |
|---|---|---|---|---|---|
| `/tours` | Browse & search tours | `GET /api/tours` | [`tours.py`](../../tourvaa-admin-backend/app/routers/tours.py) | `tours.py` | `tours`, `tour_departures` |
| `/tours/[slug]` | View tour details & itinerary | `GET /api/tours/{slug}` | [`tours.py`](../../tourvaa-admin-backend/app/routers/tours.py) | `tours.py` | `tours`, `tour_itineraries` |
| `/cart` | Manage traveler cart items | `GET /api/cart`, `POST /api/cart` | [`checkout.py`](../../tourvaa-admin-backend/app/routers/checkout.py) | `checkout.py` | `cart_items` |
| `/booking/[id]` | Traveler checkout & payment | `POST /api/bookings`, `POST /api/payments` | [`bookings.py`](../../tourvaa-admin-backend/app/routers/bookings.py) | `bookings.py` | `bookings`, `payments` |
| `/customer/bookings` | View booked trips | `GET /api/customer/bookings` | [`customers_portal.py`](../../tourvaa-admin-backend/app/routers/customers_portal.py) | `bookings.py` | `bookings`, `booking_items` |
| `/supplier/bookings` | Accept/decline bookings | `POST /api/supplier/bookings/{id}/accept` | [`bookings.py`](../../tourvaa-admin-backend/app/routers/bookings.py) | `bookings.py` | `bookings`, `suppliers` |
| `/agent/wallet` | View credit & top-up | `GET /api/agent/ledger` | [`agent_ledger.py`](../../tourvaa-admin-backend/app/routers/agent_ledger.py) | `agent_ledger.py` | `agent_wallets`, `agent_ledger_entries` |
| `/affiliate/links` | Referral links & stats | `GET /api/affiliate/links` | [`affiliate_links.py`](../../tourvaa-admin-backend/app/routers/affiliate_links.py) | `affiliates.py` | `affiliates`, `affiliate_links` |
| `/admin/users` | Manage system users | `GET /api/users`, `POST /api/users` | [`users.py`](../../tourvaa-admin-backend/app/routers/users.py) | `users.py` | `users`, `roles` |
| `/admin/reports` | Export sales reconciliations | `GET /api/reports/sales` | [`reports.py`](../../tourvaa-admin-backend/app/routers/reports.py) | `reports.py` | `bookings`, `payments` |

---

## 3. How to Safely Introduce a New API Endpoint

1. **Backend**:
   - Define Pydantic request/response schemas in `app/schemas/`.
   - Add service logic in `app/services/`.
   - Create router endpoint in `app/routers/` with permission dependency.
   - Write Pytest integration test in `tests/`.
2. **Frontend**:
   - Add TypeScript interface in `src/types/`.
   - Add API client call function in `src/lib/api/services/`.
   - Consume inside component using TanStack Query `useQuery` or `useMutation`.
