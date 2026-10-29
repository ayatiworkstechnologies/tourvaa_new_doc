# 05 — Frontend Architecture & Component Design

## 1. Next.js 16 App Router Structure

The frontend is built on **Next.js 16.4.3** (locked in `package.json`; upgraded from initial 15.5 baseline) utilizing the React 19.2.4 App Router paradigm. It is divided into logical route groups:
1. `%28public%29/`: Publicly accessible tour discovery, destination search, checkout, blog articles, and institutional pages.
2. `admin/`: Back-office administration for platform operators, tour review workflows, and financial settings.
3. `customer/`: Consumer portal for viewing booked itineraries, passenger rosters, and payments.
4. `supplier/`: Tour supplier management console for managing departures, pricing, and bookings.
5. `agent/`: B2B wholesale agent console for retail client reservations and commissions.
6. `affiliate/`: Affiliate partner dashboard for referral short-links, clicks, and wallet payouts.

---

## 2. Server-Side Route Guard (`src/proxy.ts`)

Next.js 16 replaced the traditional `middleware.ts` convention with `proxy.ts`. Tourvaa's proxy executes before any protected page HTML is sent to the browser:
- Inspects incoming requests for the `tourvaa_access` session cookie on all protected path prefixes (`/admin`, `/customer`, `/agent`, `/supplier`, `/affiliate`).
- Unauthenticated requests are immediately redirected to `/login` or `/admin/login` with the original URL preserved in `?redirect=`.
- Normalizes trailing slashes with permanent 308 redirects to avoid duplicate routing.

---

## 3. Global Context Providers

1. **`AuthProvider` ([`src/providers/AuthProvider.tsx`](../tourvaa-admin-frontend/src/providers/AuthProvider.tsx))**:
   - Manages active user authentication state, current role claims, and user profile data.
   - Listens for token invalidation events (e.g. password resets or remote session termination).
2. **`PublicSettingsProvider` ([`src/providers/PublicSettingsProvider.tsx`](../tourvaa-admin-frontend/src/providers/PublicSettingsProvider.tsx))**:
   - Fetches and caches global platform configuration, currency exchange rates, company branding, and active payment gateway toggles.
3. **`TravelStoreProvider` ([`src/providers/TravelStoreProvider.tsx`](../tourvaa-admin-frontend/src/providers/TravelStoreProvider.tsx))**:
   - Manages client-side shopping cart state, tour comparison lists, and customer wishlist items backed by `localStorage`.

---

## 4. API Communication & Proxy Rewrites

All browser HTTP requests to `/api/*` and `/storage/*` are proxied to the backend via `next.config.ts` rewrites:
```typescript
{
  source: "/api/:path*",
  destination: `${apiProxyTarget}/api/:path*`,
}
```
This ensures that the frontend communicates with the backend as a **same-origin service**, allowing secure, `httpOnly`, `SameSite=Lax` cookies to be exchanged without exposing raw JWTs to client-side JavaScript.

The complete frontend route inventory is cataloged in [`inventories/frontend-routes.md`](inventories/frontend-routes.md).
