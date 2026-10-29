# 08 — Database Schema & Data Architecture

## 1. Database Engine & ORM Configuration

- **Database Engine**: MySQL 8.0+ or MariaDB using the **InnoDB storage engine** for full ACID compliance and row-level locking.
- **ORM Framework**: SQLAlchemy 2.0 utilizing Declarative Base (`Base = declarative_base()`).
- **Connection Pooling**: Managed via `QueuePool` with configurable pool size, max overflow, and automated pool recycling to prevent stale MySQL disconnects.
- **Character Set**: `utf8mb4` with `utf8mb4_unicode_ci` collation supporting international multi-lingual text and emoji characters.

---

## 2. Relational Schema Statistics

- **Total Tables**: **138 database tables**
- **Migration Revisions**: **170 Alembic migration files** (dating from `2026-06-15` to `2026-10-28`).
- **Foreign Key Density**: High relational integrity with cascading deletion restricted on financial and audit records.

---

## 3. Core Relational Domains

1. **Identity & Access**: `users`, `roles`, `permissions`, `role_permissions`, `user_roles`, `user_sessions`, `login_history`, `audit_logs`.
2. **Geographical Master**: `countries`, `states`, `cities`, `cms_country_pages`, `cms_favourite_countries`.
3. **Tour Catalog**: `tours`, `tour_overviews`, `tour_itineraries`, `tour_pricing`, `tour_calendar`, `tour_unavailable_dates`, `tour_inclusions`, `tour_exclusions`, `tour_highlights`, `tour_gallery_images`, `tour_categories`, `tour_subcategories`.
4. **Tour Versioning**: `tour_versions`, `tour_review_comments`.
5. **Booking Hub**: `bookings`, `booking_travellers`, `booking_optional_activities`, `booking_accommodations`, `booking_extensions`, `booking_status_history`, `booking_communications`, `booking_calendar_events`.
6. **Financial & Checkout**: `payments`, `payment_transactions`, `payment_holds`, `checkout_sessions`, `invoices`, `invoice_items`.
7. **Partner Ledgers**: `suppliers`, `supplier_ledgers`, `supplier_payouts`, `agents`, `agent_ledger`.
8. **Affiliate Engine**: `affiliates`, `affiliate_links`, `affiliate_clicks`, `affiliate_attributions`, `affiliate_commission_rules`, `affiliate_conversions`, `affiliate_payouts`, `affiliate_wallet_transactions`.
9. **CMS & Engagement**: `cms_homepage_banners`, `cms_popular_destinations`, `cms_popular_tours`, `cms_blogs`, `cms_customer_reviews`, `cms_policies`.
10. **Communications & AI**: `conversations`, `messages`, `notifications`, `notification_deliveries`, `chat_faqs`, `chat_sessions`, `chat_messages`, `chat_embeddings`.

The complete schema reference of all 138 tables and columns is cataloged in [`inventories/database-tables.md`](inventories/database-tables.md).
