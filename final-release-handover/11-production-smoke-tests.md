# Chapter 11 — Production Smoke-Test Plan

## 1. Smoke Testing Methodology

Production smoke tests are non-destructive, targeted probes executed immediately following deployment to verify that all core systems are operational before opening traffic to all visitors.

---

## 2. Production Smoke Test Checklist

| Test ID | Module | Scenario / Probe | Execution Method | Safe for Prod | Expected Result |
|:---:|:---|:---|:---|:---:|:---|
| **SMK-01** | Backend Core | Health endpoint probe | `curl -f https://api.tourvaa.com/api/health` | Yes | HTTP 200 `{"status": "ok"}` |
| **SMK-02** | Frontend Core | Storefront root probe | `curl -f https://www.tourvaa.com/` | Yes | HTTP 200 with HTML document |
| **SMK-03** | API Docs | OpenAPI reflection probe | `curl -f https://api.tourvaa.com/openapi.json` | Yes | HTTP 200 response in < 50ms |
| **SMK-04** | Security | CSRF validation probe | POST to `/api/bookings` with cookie but no token | Yes | HTTP 403 Forbidden |
| **SMK-05** | Public Storefront | Curated tour listings | GET `/api/tours?is_active=true` | Yes | HTTP 200 with tour catalogue |
| **SMK-06** | Localization | Active currency exchange rates | GET `/api/currencies/active` | Yes | HTTP 200 with rate matrix |
| **SMK-07** | Public Storefront | Country selector data | GET `/api/destinations/countries` | Yes | HTTP 200 with country list |
| **SMK-08** | SEO & Metadata | Metadata tags verification | Inspect `<title>` and OpenGraph tags on `/` | Yes | Valid tags populated |
| **SMK-09** | Storefront UX | Compare page loading | Navigate to `/compare` in browser | Yes | Renders empty state cleanly |
| **SMK-10** | Auth Engine | Unauthenticated user probe | GET `/api/auth/me` without header | Yes | HTTP 401 Unauthorized |
| **SMK-11** | Auth Engine | Admin login verification | POST `/api/auth/login` with test staff account | Yes | HTTP 200 with JWT access token |
| **SMK-12** | RBAC Engine | Staff profile probe | GET `/api/auth/me` with Bearer token | Yes | HTTP 200 with user profile info |
| **SMK-13** | Back-Office | Admin dashboard navigation | Navigate to `/admin/dashboard` in browser | Yes | Dashboard KPI cards render |
| **SMK-14** | Admin Templates | Invoice templates route | Navigate to `/admin/invoice-templates` | Yes | Template page loads with layout |
| **SMK-15** | Role Portals | Customer portal dashboard | Access `/customer/dashboard` with customer login | Yes | Customer booking view loads |
| **SMK-16** | Role Portals | Supplier invoices list | Access `/supplier/invoices` with supplier login | Yes | Supplier invoices table renders |
| **SMK-17** | Realtime | WebSocket connection handshake | Connect to `wss://api.tourvaa.com/ws/notifications` | Yes | Connection accepted (101 Switching) |
| **SMK-18** | Static Assets | CDN image delivery | GET sample image from `/storage/uploads/...` | Yes | HTTP 200 with valid image header |
| **SMK-19** | Session Security | Logout token revocation | POST `/api/auth/logout` | Yes | HTTP 200 and cookies expired |
| **SMK-20** | Logging | Production error log probe | Inspect Docker log stream for fatal traces | Yes | Zero unhandled tracebacks |
