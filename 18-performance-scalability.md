# 18 — Performance, Scalability & Resource Optimization

## 1. Database Indexing & Query Optimization

- Verified indexing across high-traffic lookup columns: `users(email)`, `bookings(booking_code, customer_id, supplier_id, status)`, `tours(slug, country_id, is_active)`, and `affiliate_links(custom_alias)`.
- Eager Loading (`joinedload` / `selectinload`): High-volume endpoints explicitly eager-load relationships (e.g. `booking.travellers`, `booking.payment`) to eliminate ORM N+1 query bottlenecks.

---

## 2. Asynchronous Decoupling & Caching

- **Redis Pub/Sub**: WebSocket messages publish to Redis channel `ws:messages`, allowing horizontal scaling of Uvicorn worker processes without losing realtime message delivery.
- **Distributed Sweep Locks**: Background loops take short-lived Redis locks (`app/utils/distributed_lock.py`), ensuring that only one worker runs an hourly reminder sweep when multiple application replicas are active.
- **Next.js Image Optimization**: Media assets use modern AVIF/WebP formats with caching headers (`minimumCacheTTL: 86400`).
