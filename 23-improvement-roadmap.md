# 23 — Future Scalability & Engineering Roadmap

This roadmap identifies recommended technical enhancements and feature expansions for future development cycles.

---

## Phase 1: Architectural Refactoring & Stability (Q1 2027)
- **Service Layer Decomposition**: Split the monolithic `app/services/bookings.py` (>4,000 lines) into focused micro-services (`booking_creation.py`, `booking_status.py`, `booking_financials.py`).
- **Migration Consolidation**: Squash historical 170 migrations into a unified baseline schema migration for faster CI/CD spin-up.

---

## Phase 2: High-Availability & Global Scalability (Q2 2027)
- **Multi-Region Read Replicas**: Configure MySQL read replicas for heavy public catalog browsing traffic (`GET /api/public/tours`).
- **CDN Edge Caching**: Implement Cloudflare edge caching for static CMS pages and public tour metadata with automated cache purge webhooks.

---

## Phase 3: Enhanced Commercial & Travel Capabilities (Q3 2027)
- **Dynamic Flights & Hotel Bundling**: Integrate GDS / Amadeus flight APIs for dynamic flight-plus-tour package combinations.
- **Native Mobile Applications**: Leverage the existing REST and WebSocket API contracts to launch React Native iOS and Android mobile apps.

---

## Phase 4: Enterprise Intelligence (Q4 2027)
- **Dynamic Pricing Engine**: Implement machine-learning demand forecasting to automatically adjust tour departure pricing based on seasonal booking velocities.
