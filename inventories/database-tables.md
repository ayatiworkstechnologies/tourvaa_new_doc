# Database Table Inventory

**Total Verified Tables:** 138
**Database Engine:** MySQL 8.0+ / MariaDB (InnoDB engine)
**ORM Framework:** SQLAlchemy 2.0 (Declarative Base)
**Migration Engine:** Alembic (170 migration revisions)

| Table Name | Primary Key | Columns | Foreign Keys Count | Foreign Key References |
|---|---|---|---|---|
| `admin_modules` | `id` | 8 | 0 | - |
| `affiliate_attributions` | `id` | 13 | 4 | affiliate_link_id -> affiliate_links.id, affiliate_id -> affiliates.id, affil... |
| `affiliate_clicks` | `id` | 7 | 2 | affiliate_id -> affiliates.id, link_id -> affiliate_links.id |
| `affiliate_commission_rules` | `id` | 18 | 6 | tour_id -> tours.id, updated_by -> users.id, created_by -> users.id, category... |
| `affiliate_conversions` | `id` | 17 | 4 | affiliate_id -> affiliates.id, booking_id -> bookings.id, commission_rule_id ... |
| `affiliate_documents` | `id` | 12 | 2 | reviewed_by -> users.id, affiliate_id -> affiliates.id |
| `affiliate_invoicing` | `id` | 23 | 3 | bank_edit_unlocked_by -> users.id, country_id -> countries.id, affiliate_id -... |
| `affiliate_links` | `id` | 28 | 4 | created_by -> users.id, tour_id -> tours.id, affiliate_id -> affiliates.id, u... |
| `affiliate_marketing_info` | `id` | 9 | 1 | affiliate_id -> affiliates.id |
| `affiliate_payout_items` | `id` | 5 | 2 | payout_id -> affiliate_payouts.id, conversion_id -> affiliate_conversions.id |
| `affiliate_payout_methods` | `id` | 14 | 1 | affiliate_id -> affiliates.id |
| `affiliate_payouts` | `id` | 21 | 5 | payout_method_id -> affiliate_payout_methods.id, approved_by -> users.id, aff... |
| `affiliate_wallet_transactions` | `id` | 11 | 3 | payout_id -> affiliate_payouts.id, commission_id -> affiliate_conversions.id,... |
| `affiliates` | `id` | 23 | 5 | rejected_by -> users.id, approved_by -> users.id, city_id -> cities.id, user_... |
| `agent_business_info` | `id` | 16 | 1 | agent_id -> agents.id |
| `agent_contacts` | `id` | 13 | 1 | agent_id -> agents.id |
| `agent_documents` | `id` | 12 | 2 | agent_id -> agents.id, reviewed_by -> users.id |
| `agent_invoicing` | `id` | 24 | 4 | country_id -> countries.id, bank_edit_unlocked_by -> users.id, agent_id -> ag... |
| `agent_ledgers` | `id` | 14 | 2 | booking_id -> bookings.id, agent_id -> agents.id |
| `agent_payout_items` | `id` | 5 | 2 | payout_id -> agent_payouts.id, ledger_id -> agent_ledgers.id |
| `agent_payouts` | `id` | 18 | 5 | approved_by -> users.id, agent_id -> agents.id, paid_by -> users.id, rejected... |
| `agents` | `id` | 28 | 5 | approved_by -> users.id, rejected_by -> users.id, user_id -> users.id, city_i... |
| `api_settings` | `id` | 8 | 0 | - |
| `app_settings` | `id` | 7 | 0 | - |
| `audit_logs` | `id` | 10 | 1 | actor_user_id -> users.id |
| `booking_accommodations` | `id` | 9 | 2 | booking_id -> bookings.id, tour_accommodation_extra_id -> tour_accommodation_... |
| `booking_calendar_events` | `id` | 13 | 1 | booking_id -> bookings.id |
| `booking_communications` | `id` | 9 | 2 | booking_id -> bookings.id, sender_user_id -> users.id |
| `booking_conversations` | `id` | 12 | 3 | supplier_user_id -> users.id, booking_id -> bookings.id, initiator_user_id ->... |
| `booking_extensions` | `id` | 9 | 3 | tour_extension_id -> tour_extensions.id, booking_id -> bookings.id, extension... |
| `booking_messages` | `id` | 11 | 2 | sender_user_id -> users.id, conversation_id -> booking_conversations.id |
| `booking_modification_requests` | `id` | 14 | 3 | requester_user_id -> users.id, reviewed_by -> users.id, booking_id -> booking... |
| `booking_optional_activities` | `id` | 8 | 2 | booking_id -> bookings.id, tour_optional_activity_id -> tour_optional_activit... |
| `booking_status_history` | `id` | 9 | 2 | changed_by_user_id -> users.id, booking_id -> bookings.id |
| `booking_travellers` | `id` | 20 | 1 | booking_id -> bookings.id |
| `bookings` | `id` | 107 | 14 | affiliate_id -> affiliates.id, agent_id -> agents.id, supplier_id -> supplier... |
| `cancellation_requests` | `id` | 16 | 3 | booking_id -> bookings.id, customer_id -> customers.id, reviewed_by -> users.id |
| `chat_embeddings` | `id` | 8 | 0 | - |
| `chat_faqs` | `id` | 9 | 0 | - |
| `chat_feedback` | `id` | 7 | 2 | message_id -> chat_messages.id, session_id -> chat_sessions.id |
| `chat_messages` | `id` | 5 | 1 | session_id -> chat_sessions.id |
| `chat_sessions` | `id` | 5 | 0 | - |
| `checkout_sessions` | `id` | 13 | 5 | customer_id -> customers.id, user_id -> users.id, tour_id -> tours.id, bookin... |
| `cities` | `id` | 7 | 2 | state_id -> states.id, country_id -> countries.id |
| `cms_blogs` | `id` | 19 | 1 | created_by -> users.id |
| `cms_country_pages` | `id` | 13 | 1 | country_id -> countries.id |
| `cms_customer_reviews` | `id` | 11 | 0 | - |
| `cms_external_links` | `id` | 9 | 0 | - |
| `cms_favourite_countries` | `id` | 10 | 1 | country_id -> countries.id |
| `cms_footer_links` | `id` | 9 | 1 | section_id -> cms_footer_sections.id |
| `cms_footer_sections` | `id` | 6 | 0 | - |
| `cms_handpicked_tours` | `id` | 5 | 1 | tour_id -> tours.id |
| `cms_help_centre` | `id` | 8 | 0 | - |
| `cms_homepage_banners` | `id` | 11 | 0 | - |
| `cms_homepage_content_blocks` | `id` | 5 | 0 | - |
| `cms_pages` | `id` | 12 | 1 | footer_section_id -> cms_footer_sections.id |
| `cms_policies` | `id` | 7 | 0 | - |
| `cms_popular_destinations` | `id` | 13 | 2 | country_id -> countries.id, city_id -> cities.id |
| `cms_popular_tours` | `id` | 5 | 1 | tour_id -> tours.id |
| `cms_promotional_popups` | `id` | 13 | 0 | - |
| `cms_sitemap_entries` | `id` | 8 | 0 | - |
| `cms_tours_on_deals` | `id` | 9 | 1 | tour_id -> tours.id |
| `contact_messages` | `id` | 10 | 0 | - |
| `conversations` | `id` | 10 | 1 | participant_user_id -> users.id |
| `countries` | `id` | 10 | 0 | - |
| `currencies` | `id` | 7 | 0 | - |
| `customer_cancellation_requests` | `id` | 10 | 3 | reviewed_by -> users.id, booking_id -> bookings.id, customer_id -> customers.id |
| `customer_communications` | `id` | 10 | 3 | sent_by_user_id -> users.id, customer_id -> customers.id, booking_id -> booki... |
| `customer_saved_travellers` | `id` | 13 | 1 | customer_id -> customers.id |
| `customer_wishlist_items` | `id` | 5 | 2 | tour_id -> tours.id, user_id -> users.id |
| `customers` | `id` | 48 | 5 | user_id -> users.id, city_id -> cities.id, blocked_by -> users.id, country_id... |
| `email_logs` | `id` | 10 | 0 | - |
| `email_templates` | `id` | 7 | 0 | - |
| `external_affiliate_clicks` | `id` | 16 | 4 | tourvaa_country_id -> countries.id, agent_id -> agents.id, tourvaa_city_id ->... |
| `external_destination_mappings` | `id` | 17 | 3 | tourvaa_city_id -> cities.id, tourvaa_state_id -> states.id, tourvaa_country_... |
| `external_providers` | `id` | 16 | 0 | - |
| `invoice_items` | `id` | 9 | 1 | invoice_id -> invoices.id |
| `invoices` | `id` | 24 | 4 | booking_id -> bookings.id, payment_id -> payments.id, created_by -> users.id,... |
| `login_history` | `id` | 12 | 1 | user_id -> users.id |
| `message_replies` | `id` | 6 | 2 | sender_user_id -> users.id, communication_id -> booking_communications.id |
| `messages` | `id` | 10 | 2 | sender_user_id -> users.id, conversation_id -> conversations.id |
| `newsletter_subscribers` | `id` | 4 | 0 | - |
| `notification_deliveries` | `id` | 21 | 0 | - |
| `notification_logs` | `id` | 6 | 1 | notification_id -> notifications.id |
| `notifications` | `id` | 19 | 1 | user_id -> users.id |
| `payment_holds` | `id` | 10 | 2 | payment_id -> payments.id, booking_id -> bookings.id |
| `payment_settings` | `id` | 17 | 0 | - |
| `payment_transactions` | `id` | 10 | 3 | booking_id -> bookings.id, payment_id -> payments.id, created_by -> users.id |
| `payments` | `id` | 26 | 3 | customer_id -> customers.id, created_by -> users.id, booking_id -> bookings.id |
| `permissions` | `id` | 8 | 0 | - |
| `push_delivery_logs` | `id` | 13 | 3 | recipient_user_id -> users.id, notification_id -> notifications.id, subscript... |
| `push_subscriptions` | `id` | 12 | 1 | user_id -> users.id |
| `refund_rules` | `id` | 8 | 1 | tour_id -> tours.id |
| `report_schedules` | `id` | 8 | 1 | created_by -> users.id |
| `role_permissions` | `id` | 3 | 2 | permission_id -> permissions.id, role_id -> roles.id |
| `roles` | `id` | 6 | 0 | - |
| `smtp_settings` | `id` | 17 | 0 | - |
| `states` | `id` | 7 | 1 | country_id -> countries.id |
| `supplier_approval_history` | `id` | 7 | 2 | supplier_id -> suppliers.id, changed_by -> users.id |
| `supplier_business_info` | `id` | 15 | 1 | supplier_id -> suppliers.id |
| `supplier_contacts` | `id` | 13 | 1 | supplier_id -> suppliers.id |
| `supplier_documents` | `id` | 12 | 2 | supplier_id -> suppliers.id, reviewed_by -> users.id |
| `supplier_invoicing` | `id` | 24 | 4 | supplier_id -> suppliers.id, bank_edit_unlocked_by -> users.id, bank_country_... |
| `supplier_ledgers` | `id` | 14 | 2 | supplier_id -> suppliers.id, booking_id -> bookings.id |
| `supplier_payout_items` | `id` | 5 | 2 | payout_id -> supplier_payouts.id, ledger_id -> supplier_ledgers.id |
| `supplier_payouts` | `id` | 15 | 4 | paid_by -> users.id, initiated_by -> users.id, approved_by -> users.id, suppl... |
| `supplier_vehicles` | `id` | 17 | 2 | reviewed_by -> users.id, supplier_id -> suppliers.id |
| `suppliers` | `id` | 23 | 5 | rejected_by -> users.id, approved_by -> users.id, city_id -> cities.id, count... |
| `tour_accommodation_extras` | `id` | 14 | 1 | tour_id -> tours.id |
| `tour_availability_configs` | `id` | 15 | 1 | tour_id -> tours.id |
| `tour_calendar` | `id` | 11 | 1 | tour_id -> tours.id |
| `tour_categories` | `id` | 8 | 0 | - |
| `tour_date_prices` | `id` | 8 | 1 | tour_id -> tours.id |
| `tour_discount_history` | `id` | 12 | 2 | changed_by -> users.id, discount_id -> tour_discounts.id |
| `tour_discount_redemptions` | `id` | 6 | 2 | discount_id -> tour_discounts.id, booking_id -> bookings.id |
| `tour_discounts` | `id` | 19 | 3 | tour_id -> tours.id, country_id -> countries.id, category_id -> tour_categori... |
| `tour_exclusions` | `id` | 9 | 1 | tour_id -> tours.id |
| `tour_extensions` | `id` | 14 | 2 | tour_id -> tours.id, extension_tour_id -> tours.id |
| `tour_gallery_images` | `id` | 11 | 1 | tour_id -> tours.id |
| `tour_group_discount_tiers` | `id` | 10 | 1 | tour_id -> tours.id |
| `tour_highlights` | `id` | 9 | 1 | tour_id -> tours.id |
| `tour_inclusions` | `id` | 9 | 1 | tour_id -> tours.id |
| `tour_itineraries` | `id` | 25 | 1 | tour_id -> tours.id |
| `tour_optional_activities` | `id` | 15 | 1 | tour_id -> tours.id |
| `tour_overviews` | `id` | 20 | 1 | tour_id -> tours.id |
| `tour_pricing` | `id` | 19 | 1 | tour_id -> tours.id |
| `tour_review_comments` | `id` | 13 | 4 | tour_id -> tours.id, resolved_by -> users.id, version_id -> tour_versions.id,... |
| `tour_reviews` | `id` | 9 | 3 | customer_id -> customers.id, booking_id -> bookings.id, tour_id -> tours.id |
| `tour_similar_tours` | `id` | 6 | 2 | tour_id -> tours.id, similar_tour_id -> tours.id |
| `tour_subcategories` | `id` | 9 | 1 | category_id -> tour_categories.id |
| `tour_subcategory_map` | `id` | 4 | 2 | tour_id -> tours.id, subcategory_id -> tour_subcategories.id |
| `tour_unavailable_dates` | `id` | 6 | 1 | tour_id -> tours.id |
| `tour_versions` | `id` | 12 | 3 | tour_id -> tours.id, reviewed_by -> users.id, submitted_by -> users.id |
| `tours` | `id` | 58 | 7 | state_id -> states.id, category_id -> tour_categories.id, city_id -> cities.i... |
| `user_roles` | `id` | 4 | 2 | user_id -> users.id, role_id -> roles.id |
| `user_sessions` | `id` | 10 | 1 | user_id -> users.id |
| `user_status_history` | `id` | 7 | 2 | changed_by -> users.id, user_id -> users.id |
| `users` | `id` | 44 | 3 | role_id -> roles.id, deactivated_by -> users.id, admin_verified_by -> users.id |

## Detailed Table Schema Reference

### `admin_modules`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `name` | `VARCHAR(100)` | False | False | - |
| `slug` | `VARCHAR(100)` | False | False | - |
| `description` | `VARCHAR(255)` | False | False |  |
| `is_active` | `BOOLEAN` | False | False | True |
| `is_system` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `affiliate_attributions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `affiliate_id` | `INTEGER` | False | False | - |
| `affiliate_link_id` | `INTEGER` | False | False | - |
| `affiliate_click_id` | `INTEGER` | True | False | - |
| `visitor_id` | `VARCHAR(64)` | False | False | - |
| `session_id` | `VARCHAR(64)` | True | False | - |
| `booking_id` | `INTEGER` | True | False | - |
| `attribution_model` | `VARCHAR(20)` | False | False | last_click |
| `attributed_at` | `DATETIME` | True | False | - |
| `expires_at` | `DATETIME` | False | False | - |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `affiliate_link_id` references `affiliate_links.id`
- Column `affiliate_id` references `affiliates.id`
- Column `affiliate_click_id` references `affiliate_clicks.id`
- Column `booking_id` references `bookings.id`

### `affiliate_clicks`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `link_id` | `INTEGER` | False | False | - |
| `affiliate_id` | `INTEGER` | False | False | - |
| `ip_address` | `VARCHAR(50)` | True | False | - |
| `user_agent` | `VARCHAR(500)` | True | False | - |
| `referrer` | `VARCHAR(500)` | True | False | - |
| `clicked_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `affiliate_id` references `affiliates.id`
- Column `link_id` references `affiliate_links.id`

### `affiliate_commission_rules`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `name` | `VARCHAR(150)` | True | False | - |
| `affiliate_id` | `INTEGER` | True | False | - |
| `tour_id` | `INTEGER` | True | False | - |
| `category_id` | `INTEGER` | True | False | - |
| `affiliate_link_id` | `INTEGER` | True | False | - |
| `commission_type` | `VARCHAR(20)` | False | False | percentage |
| `percentage` | `NUMERIC(5, 2)` | False | False | 0 |
| `fixed_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `valid_from` | `DATETIME` | True | False | - |
| `valid_until` | `DATETIME` | True | False | - |
| `priority` | `INTEGER` | False | False | 0 |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_by` | `INTEGER` | True | False | - |
| `updated_by` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`
- Column `updated_by` references `users.id`
- Column `created_by` references `users.id`
- Column `category_id` references `tour_categories.id`
- Column `affiliate_id` references `affiliates.id`
- Column `affiliate_link_id` references `affiliate_links.id`

### `affiliate_conversions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `link_id` | `INTEGER` | False | False | - |
| `affiliate_id` | `INTEGER` | False | False | - |
| `booking_id` | `INTEGER` | False | False | - |
| `commission_rule_id` | `INTEGER` | True | False | - |
| `booking_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `eligible_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `commission_percentage` | `NUMERIC(5, 2)` | False | False | 0 |
| `commission_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `original_commission` | `NUMERIC(12, 2)` | True | False | - |
| `adjustment_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `final_commission` | `NUMERIC(12, 2)` | True | False | - |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `status` | `VARCHAR(30)` | False | False | pending |
| `approved_at` | `DATETIME` | True | False | - |
| `available_at` | `DATETIME` | True | False | - |
| `converted_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `affiliate_id` references `affiliates.id`
- Column `booking_id` references `bookings.id`
- Column `commission_rule_id` references `affiliate_commission_rules.id`
- Column `link_id` references `affiliate_links.id`

### `affiliate_documents`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `affiliate_id` | `INTEGER` | False | False | - |
| `document_type` | `VARCHAR(100)` | False | False | - |
| `document_name` | `VARCHAR(150)` | False | False | - |
| `file_path` | `VARCHAR(255)` | False | False | - |
| `file_size` | `INTEGER` | False | False | 0 |
| `mime_type` | `VARCHAR(100)` | False | False |  |
| `status` | `VARCHAR(20)` | False | False | pending |
| `rejection_reason` | `VARCHAR(255)` | True | False | - |
| `uploaded_at` | `DATETIME` | True | False | - |
| `reviewed_at` | `DATETIME` | True | False | - |
| `reviewed_by` | `INTEGER` | True | False | - |

**Foreign Keys:**
- Column `reviewed_by` references `users.id`
- Column `affiliate_id` references `affiliates.id`

### `affiliate_invoicing`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `affiliate_id` | `INTEGER` | False | False | - |
| `contact_name` | `VARCHAR(150)` | False | False |  |
| `email` | `VARCHAR(150)` | False | False |  |
| `phone` | `VARCHAR(30)` | False | False |  |
| `preferred_payment_method` | `VARCHAR(30)` | False | False |  |
| `account_name` | `VARCHAR(150)` | False | False |  |
| `account_number` | `VARCHAR(100)` | False | False |  |
| `bank_name` | `VARCHAR(150)` | False | False |  |
| `bank_branch` | `VARCHAR(150)` | False | False |  |
| `swift_code` | `VARCHAR(50)` | False | False |  |
| `iban` | `VARCHAR(100)` | False | False |  |
| `country_id` | `INTEGER` | True | False | - |
| `tax_number` | `VARCHAR(100)` | False | False |  |
| `billing_address` | `TEXT` | True | False | - |
| `billing_city` | `VARCHAR(100)` | False | False |  |
| `billing_state` | `VARCHAR(100)` | False | False |  |
| `billing_postal_code` | `VARCHAR(30)` | False | False |  |
| `bank_edit_requested_at` | `DATETIME` | True | False | - |
| `bank_edit_unlocked_at` | `DATETIME` | True | False | - |
| `bank_edit_unlocked_by` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `bank_edit_unlocked_by` references `users.id`
- Column `country_id` references `countries.id`
- Column `affiliate_id` references `affiliates.id`

### `affiliate_links`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `affiliate_id` | `INTEGER` | False | False | - |
| `ref_code` | `VARCHAR(60)` | False | False | - |
| `destination_url` | `VARCHAR(500)` | True | False | - |
| `label` | `VARCHAR(120)` | True | False | - |
| `is_active` | `BOOLEAN` | False | False | True |
| `link_type` | `VARCHAR(20)` | False | False | custom |
| `tour_id` | `INTEGER` | True | False | - |
| `campaign_name` | `VARCHAR(150)` | True | False | - |
| `utm_source` | `VARCHAR(100)` | True | False | - |
| `utm_medium` | `VARCHAR(100)` | True | False | - |
| `utm_campaign` | `VARCHAR(100)` | True | False | - |
| `utm_content` | `VARCHAR(100)` | True | False | - |
| `utm_term` | `VARCHAR(100)` | True | False | - |
| `custom_alias` | `VARCHAR(100)` | True | False | - |
| `commission_type_override` | `VARCHAR(20)` | True | False | - |
| `commission_percentage_override` | `NUMERIC(5, 2)` | True | False | - |
| `commission_fixed_override` | `NUMERIC(12, 2)` | True | False | - |
| `attribution_model` | `VARCHAR(20)` | False | False | last_click |
| `attribution_window_days` | `INTEGER` | False | False | 30 |
| `valid_from` | `DATETIME` | True | False | - |
| `valid_until` | `DATETIME` | True | False | - |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_by` | `INTEGER` | True | False | - |
| `updated_by` | `INTEGER` | True | False | - |
| `deleted_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `created_by` references `users.id`
- Column `tour_id` references `tours.id`
- Column `affiliate_id` references `affiliates.id`
- Column `updated_by` references `users.id`

### `affiliate_marketing_info`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `affiliate_id` | `INTEGER` | False | False | - |
| `promotion_methods` | `TEXT` | False | False |  |
| `estimated_monthly_bookings` | `INTEGER` | False | False | 0 |
| `existing_audience_size` | `INTEGER` | False | False | 0 |
| `social_media_profiles` | `TEXT` | False | False |  |
| `existing_travel_platforms_used` | `TEXT` | False | False |  |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `affiliate_id` references `affiliates.id`

### `affiliate_payout_items`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `payout_id` | `INTEGER` | False | False | - |
| `conversion_id` | `INTEGER` | False | False | - |
| `amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `payout_id` references `affiliate_payouts.id`
- Column `conversion_id` references `affiliate_conversions.id`

### `affiliate_payout_methods`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `affiliate_id` | `INTEGER` | False | False | - |
| `method_type` | `VARCHAR(30)` | False | False | bank_transfer |
| `account_holder_name` | `VARCHAR(150)` | False | False |  |
| `bank_name` | `VARCHAR(150)` | False | False |  |
| `account_number` | `VARCHAR(100)` | False | False |  |
| `ifsc` | `VARCHAR(30)` | False | False |  |
| `swift_code` | `VARCHAR(30)` | False | False |  |
| `bank_country` | `VARCHAR(100)` | False | False |  |
| `paypal_email` | `VARCHAR(150)` | False | False |  |
| `is_default` | `BOOLEAN` | False | False | False |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `affiliate_id` references `affiliates.id`

### `affiliate_payouts`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `payout_code` | `VARCHAR(30)` | True | False | - |
| `affiliate_id` | `INTEGER` | False | False | - |
| `payout_method_id` | `INTEGER` | True | False | - |
| `total_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `payment_method` | `VARCHAR(50)` | False | False | bank_transfer |
| `reference_number` | `VARCHAR(150)` | True | False | - |
| `status` | `VARCHAR(30)` | False | False | pending |
| `notes` | `TEXT` | True | False | - |
| `requested_at` | `DATETIME` | True | False | - |
| `approved_at` | `DATETIME` | True | False | - |
| `approved_by` | `INTEGER` | True | False | - |
| `rejected_at` | `DATETIME` | True | False | - |
| `rejected_by` | `INTEGER` | True | False | - |
| `rejection_reason` | `VARCHAR(255)` | True | False | - |
| `processing_at` | `DATETIME` | True | False | - |
| `initiated_by` | `INTEGER` | True | False | - |
| `paid_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `payout_method_id` references `affiliate_payout_methods.id`
- Column `approved_by` references `users.id`
- Column `affiliate_id` references `affiliates.id`
- Column `initiated_by` references `users.id`
- Column `rejected_by` references `users.id`

### `affiliate_wallet_transactions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `affiliate_id` | `INTEGER` | False | False | - |
| `commission_id` | `INTEGER` | True | False | - |
| `payout_id` | `INTEGER` | True | False | - |
| `transaction_type` | `VARCHAR(30)` | False | False | - |
| `amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `reference_type` | `VARCHAR(30)` | True | False | - |
| `reference_id` | `INTEGER` | True | False | - |
| `description` | `VARCHAR(255)` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `payout_id` references `affiliate_payouts.id`
- Column `commission_id` references `affiliate_conversions.id`
- Column `affiliate_id` references `affiliates.id`

### `affiliates`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `user_id` | `INTEGER` | True | False | - |
| `affiliate_code` | `VARCHAR(30)` | True | False | - |
| `business_type` | `VARCHAR(75)` | False | False |  |
| `name` | `VARCHAR(150)` | False | False | - |
| `email` | `VARCHAR(150)` | False | False | - |
| `phone` | `VARCHAR(30)` | False | False |  |
| `website_url` | `VARCHAR(255)` | False | False |  |
| `country_id` | `INTEGER` | True | False | - |
| `city_id` | `INTEGER` | True | False | - |
| `status` | `VARCHAR(20)` | False | False | inactive |
| `approval_status` | `VARCHAR(30)` | False | False | pending |
| `commission_percentage` | `NUMERIC(5, 2)` | False | False | 0 |
| `rejection_reason` | `VARCHAR(255)` | True | False | - |
| `admin_comments` | `TEXT` | True | False | - |
| `api_link` | `VARCHAR(255)` | False | False |  |
| `approved_at` | `DATETIME` | True | False | - |
| `approved_by` | `INTEGER` | True | False | - |
| `rejected_at` | `DATETIME` | True | False | - |
| `rejected_by` | `INTEGER` | True | False | - |
| `commission_accepted_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `rejected_by` references `users.id`
- Column `approved_by` references `users.id`
- Column `city_id` references `cities.id`
- Column `user_id` references `users.id`
- Column `country_id` references `countries.id`

### `agent_business_info`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `agent_id` | `INTEGER` | False | False | - |
| `years_in_business` | `INTEGER` | False | False | 0 |
| `certificate_of_incorporation` | `VARCHAR(255)` | False | False |  |
| `monthly_customers_count` | `INTEGER` | False | False | 0 |
| `target_market` | `VARCHAR(255)` | False | False |  |
| `destinations_sold` | `TEXT` | False | False |  |
| `iata_registration_number` | `VARCHAR(100)` | False | False |  |
| `gst_tax_number` | `VARCHAR(100)` | False | False |  |
| `trading_name` | `VARCHAR(150)` | False | False |  |
| `business_email` | `VARCHAR(150)` | False | False |  |
| `website_url` | `VARCHAR(255)` | False | False |  |
| `business_registration_number` | `VARCHAR(100)` | False | False |  |
| `approval_status` | `VARCHAR(30)` | False | False | pending |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `agent_id` references `agents.id`

### `agent_contacts`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `agent_id` | `INTEGER` | False | False | - |
| `contact_name` | `VARCHAR(150)` | False | False | - |
| `first_name` | `VARCHAR(75)` | False | False |  |
| `last_name` | `VARCHAR(75)` | False | False |  |
| `designation` | `VARCHAR(100)` | False | False |  |
| `phone` | `VARCHAR(30)` | False | False |  |
| `email` | `VARCHAR(150)` | False | False |  |
| `alternate_phone` | `VARCHAR(30)` | False | False |  |
| `preferred_contact_method` | `VARCHAR(20)` | False | False |  |
| `is_primary` | `BOOLEAN` | False | False | False |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `agent_id` references `agents.id`

### `agent_documents`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `agent_id` | `INTEGER` | False | False | - |
| `document_type` | `VARCHAR(100)` | False | False | - |
| `document_name` | `VARCHAR(150)` | False | False | - |
| `file_path` | `VARCHAR(255)` | False | False | - |
| `file_size` | `INTEGER` | False | False | 0 |
| `mime_type` | `VARCHAR(100)` | False | False |  |
| `status` | `VARCHAR(20)` | False | False | pending |
| `rejection_reason` | `VARCHAR(255)` | True | False | - |
| `uploaded_at` | `DATETIME` | True | False | - |
| `reviewed_at` | `DATETIME` | True | False | - |
| `reviewed_by` | `INTEGER` | True | False | - |

**Foreign Keys:**
- Column `agent_id` references `agents.id`
- Column `reviewed_by` references `users.id`

### `agent_invoicing`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `agent_id` | `INTEGER` | False | False | - |
| `contact_name` | `VARCHAR(150)` | False | False |  |
| `email` | `VARCHAR(150)` | False | False |  |
| `phone` | `VARCHAR(30)` | False | False |  |
| `preferred_payment_method` | `VARCHAR(30)` | False | False |  |
| `account_name` | `VARCHAR(150)` | False | False |  |
| `account_number` | `VARCHAR(100)` | False | False |  |
| `bank_name` | `VARCHAR(150)` | False | False |  |
| `bank_branch` | `VARCHAR(150)` | False | False |  |
| `swift_code` | `VARCHAR(50)` | False | False |  |
| `iban` | `VARCHAR(100)` | False | False |  |
| `country_id` | `INTEGER` | True | False | - |
| `bank_country_id` | `INTEGER` | True | False | - |
| `tax_number` | `VARCHAR(100)` | False | False |  |
| `billing_address` | `TEXT` | True | False | - |
| `billing_city` | `VARCHAR(100)` | False | False |  |
| `billing_state` | `VARCHAR(100)` | False | False |  |
| `billing_postal_code` | `VARCHAR(30)` | False | False |  |
| `bank_edit_requested_at` | `DATETIME` | True | False | - |
| `bank_edit_unlocked_at` | `DATETIME` | True | False | - |
| `bank_edit_unlocked_by` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `country_id` references `countries.id`
- Column `bank_edit_unlocked_by` references `users.id`
- Column `agent_id` references `agents.id`
- Column `bank_country_id` references `countries.id`

### `agent_ledgers`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `agent_id` | `INTEGER` | False | False | - |
| `booking_id` | `INTEGER` | False | False | - |
| `gross_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `commission_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `commission_percentage` | `NUMERIC(5, 2)` | False | False | 0 |
| `net_payable` | `NUMERIC(12, 2)` | False | False | 0 |
| `amount_paid` | `NUMERIC(12, 2)` | False | False | 0 |
| `amount_pending` | `NUMERIC(12, 2)` | False | False | 0 |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `status` | `VARCHAR(30)` | False | False | pending |
| `notes` | `TEXT` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `booking_id` references `bookings.id`
- Column `agent_id` references `agents.id`

### `agent_payout_items`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `payout_id` | `INTEGER` | False | False | - |
| `ledger_id` | `INTEGER` | False | False | - |
| `amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `payout_id` references `agent_payouts.id`
- Column `ledger_id` references `agent_ledgers.id`

### `agent_payouts`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `payout_code` | `VARCHAR(30)` | True | False | - |
| `agent_id` | `INTEGER` | False | False | - |
| `total_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `payment_method` | `VARCHAR(50)` | False | False | bank_transfer |
| `reference_number` | `VARCHAR(150)` | True | False | - |
| `status` | `VARCHAR(30)` | False | False | pending |
| `notes` | `TEXT` | True | False | - |
| `initiated_by` | `INTEGER` | True | False | - |
| `approved_by` | `INTEGER` | True | False | - |
| `rejected_by` | `INTEGER` | True | False | - |
| `rejected_at` | `DATETIME` | True | False | - |
| `rejection_reason` | `VARCHAR(255)` | True | False | - |
| `paid_by` | `INTEGER` | True | False | - |
| `paid_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `approved_by` references `users.id`
- Column `agent_id` references `agents.id`
- Column `paid_by` references `users.id`
- Column `rejected_by` references `users.id`
- Column `initiated_by` references `users.id`

### `agents`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `user_id` | `INTEGER` | True | False | - |
| `agent_code` | `VARCHAR(30)` | True | False | - |
| `agent_name` | `VARCHAR(150)` | False | False | - |
| `agent_type` | `VARCHAR(75)` | False | False |  |
| `country_id` | `INTEGER` | True | False | - |
| `city_id` | `INTEGER` | True | False | - |
| `currency` | `VARCHAR(10)` | True | False | - |
| `years_in_operation` | `INTEGER` | False | False | 0 |
| `status` | `VARCHAR(20)` | False | False | inactive |
| `approval_status` | `VARCHAR(30)` | False | False | pending |
| `rejection_reason` | `VARCHAR(255)` | True | False | - |
| `admin_comments` | `TEXT` | True | False | - |
| `pending_requirements` | `TEXT` | True | False | - |
| `discount_type` | `VARCHAR(20)` | True | False | - |
| `discount_value` | `NUMERIC(12, 2)` | False | False | 0 |
| `commission_request_type` | `VARCHAR(20)` | True | False | - |
| `commission_request_value` | `NUMERIC(12, 2)` | True | False | - |
| `commission_request_status` | `VARCHAR(20)` | True | False | - |
| `commission_requested_at` | `DATETIME` | True | False | - |
| `commission_reviewed_at` | `DATETIME` | True | False | - |
| `approved_at` | `DATETIME` | True | False | - |
| `approved_by` | `INTEGER` | True | False | - |
| `rejected_at` | `DATETIME` | True | False | - |
| `rejected_by` | `INTEGER` | True | False | - |
| `commission_accepted_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `approved_by` references `users.id`
- Column `rejected_by` references `users.id`
- Column `user_id` references `users.id`
- Column `city_id` references `cities.id`
- Column `country_id` references `countries.id`

### `api_settings`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `api_name` | `VARCHAR(100)` | False | False | - |
| `api_key` | `TEXT` | True | False | - |
| `api_secret` | `TEXT` | True | False | - |
| `api_url` | `TEXT` | True | False | - |
| `is_enabled` | `BOOLEAN` | False | False | False |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `app_settings`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `key` | `VARCHAR(100)` | False | False | - |
| `value` | `TEXT` | True | False | - |
| `label` | `VARCHAR(150)` | False | False | - |
| `group` | `VARCHAR(80)` | False | False | general |
| `is_public` | `BOOLEAN` | True | False | False |
| `updated_at` | `DATETIME` | True | False | - |

### `audit_logs`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `actor_user_id` | `INTEGER` | True | False | - |
| `action` | `VARCHAR(100)` | False | False | - |
| `entity_type` | `VARCHAR(100)` | False | False | - |
| `entity_id` | `INTEGER` | True | False | - |
| `old_values` | `JSON` | True | False | - |
| `new_values` | `JSON` | True | False | - |
| `ip_address` | `VARCHAR(100)` | True | False | - |
| `user_agent` | `VARCHAR(255)` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `actor_user_id` references `users.id`

### `booking_accommodations`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `booking_id` | `INTEGER` | False | False | - |
| `tour_accommodation_extra_id` | `INTEGER` | True | False | - |
| `accommodation_name_snapshot` | `VARCHAR(255)` | False | False | - |
| `quantity` | `INTEGER` | False | False | 1 |
| `price_type` | `VARCHAR(30)` | False | False | per_person |
| `unit_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `total_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `booking_id` references `bookings.id`
- Column `tour_accommodation_extra_id` references `tour_accommodation_extras.id`

### `booking_calendar_events`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `booking_id` | `INTEGER` | False | False | - |
| `provider` | `VARCHAR(30)` | False | False | internal |
| `external_event_id` | `VARCHAR(255)` | True | False | - |
| `event_url` | `VARCHAR(500)` | True | False | - |
| `ical_uid` | `VARCHAR(100)` | True | False | - |
| `ics_file_path` | `VARCHAR(255)` | True | False | - |
| `sync_status` | `VARCHAR(30)` | False | False | synced |
| `sync_error` | `TEXT` | True | False | - |
| `retry_count` | `INTEGER` | False | False | 0 |
| `last_synced_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `booking_id` references `bookings.id`

### `booking_communications`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `booking_id` | `INTEGER` | False | False | - |
| `sender_user_id` | `INTEGER` | True | False | - |
| `sender_type` | `VARCHAR(30)` | False | False | admin |
| `message_type` | `VARCHAR(30)` | False | False | admin_message |
| `subject` | `VARCHAR(255)` | False | False |  |
| `message` | `TEXT` | False | False | - |
| `visibility` | `VARCHAR(30)` | False | False | internal |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `booking_id` references `bookings.id`
- Column `sender_user_id` references `users.id`

### `booking_conversations`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `booking_id` | `INTEGER` | False | False | - |
| `initiator_role` | `VARCHAR(20)` | False | False | - |
| `initiator_user_id` | `INTEGER` | False | False | - |
| `supplier_user_id` | `INTEGER` | False | False | - |
| `status` | `VARCHAR(20)` | False | False | open |
| `last_message_at` | `DATETIME` | True | False | - |
| `last_message_preview` | `VARCHAR(300)` | True | False | - |
| `initiator_unread_count` | `INTEGER` | False | False | 0 |
| `supplier_unread_count` | `INTEGER` | False | False | 0 |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `supplier_user_id` references `users.id`
- Column `booking_id` references `bookings.id`
- Column `initiator_user_id` references `users.id`

### `booking_extensions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `booking_id` | `INTEGER` | False | False | - |
| `tour_extension_id` | `INTEGER` | True | False | - |
| `extension_tour_id` | `INTEGER` | True | False | - |
| `extension_name_snapshot` | `VARCHAR(255)` | False | False | - |
| `quantity` | `INTEGER` | False | False | 1 |
| `unit_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `total_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_extension_id` references `tour_extensions.id`
- Column `booking_id` references `bookings.id`
- Column `extension_tour_id` references `tours.id`

### `booking_messages`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `conversation_id` | `INTEGER` | False | False | - |
| `sender_user_id` | `INTEGER` | True | False | - |
| `sender_role` | `VARCHAR(20)` | False | False | - |
| `recipient_role` | `VARCHAR(20)` | True | False | - |
| `body` | `TEXT` | False | False | - |
| `is_deleted` | `BOOLEAN` | False | False | False |
| `deleted_at` | `DATETIME` | True | False | - |
| `delivered_at` | `DATETIME` | True | False | - |
| `read_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `sender_user_id` references `users.id`
- Column `conversation_id` references `booking_conversations.id`

### `booking_modification_requests`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `booking_id` | `INTEGER` | False | False | - |
| `status` | `VARCHAR(20)` | False | False | pending |
| `requester_user_id` | `INTEGER` | False | False | - |
| `requester_type` | `VARCHAR(30)` | False | False | - |
| `proposed_changes` | `JSON` | False | False | - |
| `original_values` | `JSON` | False | False | - |
| `reason` | `TEXT` | True | False | - |
| `reviewed_by` | `INTEGER` | True | False | - |
| `decision_reason` | `TEXT` | True | False | - |
| `decision_history` | `JSON` | True | False | - |
| `reviewed_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `requester_user_id` references `users.id`
- Column `reviewed_by` references `users.id`
- Column `booking_id` references `bookings.id`

### `booking_optional_activities`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `booking_id` | `INTEGER` | False | False | - |
| `tour_optional_activity_id` | `INTEGER` | True | False | - |
| `activity_name_snapshot` | `VARCHAR(255)` | False | False | - |
| `quantity` | `INTEGER` | False | False | 1 |
| `unit_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `total_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `booking_id` references `bookings.id`
- Column `tour_optional_activity_id` references `tour_optional_activities.id`

### `booking_status_history`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `booking_id` | `INTEGER` | False | False | - |
| `old_status` | `VARCHAR(30)` | True | False | - |
| `new_status` | `VARCHAR(30)` | False | False | - |
| `changed_by_user_id` | `INTEGER` | True | False | - |
| `change_source` | `VARCHAR(30)` | False | False | admin |
| `reason` | `TEXT` | True | False | - |
| `metadata_json` | `JSON` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `changed_by_user_id` references `users.id`
- Column `booking_id` references `bookings.id`

### `booking_travellers`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `booking_id` | `INTEGER` | False | False | - |
| `traveller_type` | `VARCHAR(20)` | False | False | - |
| `first_name` | `VARCHAR(100)` | False | False |  |
| `last_name` | `VARCHAR(100)` | False | False |  |
| `full_name` | `VARCHAR(220)` | False | False |  |
| `date_of_birth` | `DATETIME` | True | False | - |
| `age` | `INTEGER` | True | False | - |
| `gender` | `VARCHAR(30)` | True | False | - |
| `nationality` | `VARCHAR(100)` | True | False | - |
| `passport_number` | `VARCHAR(100)` | True | False | - |
| `passport_expiry_date` | `DATETIME` | True | False | - |
| `email` | `VARCHAR(150)` | True | False | - |
| `phone` | `VARCHAR(50)` | True | False | - |
| `is_primary_contact` | `INTEGER` | False | False | 0 |
| `special_requirements` | `TEXT` | True | False | - |
| `pickup_location` | `VARCHAR(255)` | True | False | - |
| `emergency_contact` | `VARCHAR(150)` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `booking_id` references `bookings.id`

### `bookings`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `booking_code` | `VARCHAR(30)` | True | False | - |
| `customer_id` | `INTEGER` | True | False | - |
| `tour_id` | `INTEGER` | True | False | - |
| `tour_calendar_id` | `INTEGER` | True | False | - |
| `supplier_id` | `INTEGER` | True | False | - |
| `agent_id` | `INTEGER` | True | False | - |
| `affiliate_id` | `INTEGER` | True | False | - |
| `affiliate_ref_code` | `VARCHAR(60)` | True | False | - |
| `affiliate_attribution_id` | `INTEGER` | True | False | - |
| `created_by` | `INTEGER` | True | False | - |
| `booked_by_user_id` | `INTEGER` | True | False | - |
| `booking_source` | `VARCHAR(30)` | False | False | admin |
| `country_id` | `INTEGER` | True | False | - |
| `city_id` | `INTEGER` | True | False | - |
| `tour_name` | `VARCHAR(255)` | False | False |  |
| `tour_date` | `VARCHAR(30)` | False | False |  |
| `country` | `VARCHAR(100)` | False | False |  |
| `supplier_name` | `VARCHAR(150)` | False | False |  |
| `tour_start_date` | `DATETIME` | True | False | - |
| `tour_end_date` | `DATETIME` | True | False | - |
| `no_of_adults` | `INTEGER` | False | False | 1 |
| `no_of_children` | `INTEGER` | False | False | 0 |
| `no_of_infants` | `INTEGER` | False | False | 0 |
| `no_of_rooms` | `INTEGER` | True | False | - |
| `adults_count` | `INTEGER` | False | False | 1 |
| `children_count` | `INTEGER` | False | False | 0 |
| `total_travellers` | `INTEGER` | False | False | 1 |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `total_cost` | `NUMERIC(12, 2)` | False | False | 0 |
| `base_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `optional_activity_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `accommodation_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `extension_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `non_commissionable_addon_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `cost_plus_customer_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `cost_plus_supplier_payable` | `NUMERIC(12, 2)` | False | False | 0 |
| `discount_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `promo_code` | `VARCHAR(100)` | True | False | - |
| `group_discount_tier_id` | `INTEGER` | True | False | - |
| `group_discount_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `group_discount_funded_by` | `VARCHAR(20)` | True | False | - |
| `promo_discount_funded_by` | `VARCHAR(20)` | True | False | - |
| `tax_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `surcharge_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `service_fee_amount` | `NUMERIC(12, 2)` | True | False | - |
| `gateway_fee_amount` | `NUMERIC(12, 2)` | True | False | - |
| `final_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `agent_net_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `agent_markup` | `NUMERIC(12, 2)` | False | False | 0 |
| `customer_selling_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `amount_paid` | `NUMERIC(12, 2)` | False | False | 0 |
| `amount_pending` | `NUMERIC(12, 2)` | False | False | 0 |
| `price_source` | `VARCHAR(20)` | True | False | - |
| `date_price_id` | `INTEGER` | True | False | - |
| `adult_unit_price` | `NUMERIC(12, 2)` | True | False | - |
| `child_unit_price` | `NUMERIC(12, 2)` | True | False | - |
| `infant_unit_price` | `NUMERIC(12, 2)` | True | False | - |
| `single_supplement_amount` | `NUMERIC(12, 2)` | True | False | - |
| `group_discount_base_amount` | `NUMERIC(12, 2)` | True | False | - |
| `group_discount_percentage` | `NUMERIC(7, 4)` | True | False | - |
| `admin_markup_percentage` | `NUMERIC(5, 2)` | True | False | - |
| `supplier_base_amount` | `NUMERIC(12, 2)` | True | False | - |
| `admin_markup_amount` | `NUMERIC(12, 2)` | True | False | - |
| `commission_base_amount` | `NUMERIC(12, 2)` | True | False | - |
| `supplier_gross_amount` | `NUMERIC(12, 2)` | True | False | - |
| `supplier_discount_share_amount` | `NUMERIC(12, 2)` | True | False | - |
| `tourvaa_discount_share_amount` | `NUMERIC(12, 2)` | True | False | - |
| `tourvaa_gross_revenue` | `NUMERIC(12, 2)` | True | False | - |
| `agent_commission_base_amount` | `NUMERIC(12, 2)` | True | False | - |
| `affiliate_commission_base_amount` | `NUMERIC(12, 2)` | True | False | - |
| `financials_locked_at` | `DATETIME` | True | False | - |
| `tourvaa_commission_percentage` | `NUMERIC(5, 2)` | True | False | - |
| `tourvaa_commission_amount` | `NUMERIC(12, 2)` | True | False | - |
| `supplier_net_payable` | `NUMERIC(12, 2)` | True | False | - |
| `agent_commission_percentage` | `NUMERIC(5, 2)` | True | False | - |
| `agent_commission_amount` | `NUMERIC(12, 2)` | True | False | - |
| `affiliate_commission_percentage` | `NUMERIC(5, 2)` | True | False | - |
| `affiliate_commission_amount` | `NUMERIC(12, 2)` | True | False | - |
| `tourvaa_net_revenue` | `NUMERIC(12, 2)` | True | False | - |
| `pricing_slab_id` | `INTEGER` | True | False | - |
| `supplier_price` | `NUMERIC(12, 2)` | True | False | - |
| `supplier_currency` | `VARCHAR(10)` | True | False | - |
| `tourvaa_selling_price` | `NUMERIC(12, 2)` | True | False | - |
| `display_currency` | `VARCHAR(10)` | True | False | - |
| `exchange_rate` | `NUMERIC(14, 6)` | True | False | - |
| `exchange_rate_source` | `VARCHAR(30)` | True | False | - |
| `exchange_rate_captured_at` | `DATETIME` | True | False | - |
| `converted_customer_amount` | `NUMERIC(12, 2)` | True | False | - |
| `booking_status` | `VARCHAR(30)` | False | False | draft |
| `supplier_acceptance_status` | `VARCHAR(30)` | False | False | not_assigned |
| `payment_status` | `VARCHAR(30)` | False | False | unpaid |
| `payment_type` | `VARCHAR(30)` | False | False | full |
| `agent_payment_method` | `VARCHAR(30)` | True | False | - |
| `agent_reference` | `VARCHAR(100)` | True | False | - |
| `agent_hidden_at` | `DATETIME` | True | False | - |
| `notes` | `TEXT` | True | False | - |
| `customer_notes` | `TEXT` | True | False | - |
| `admin_notes` | `TEXT` | True | False | - |
| `cancellation_reason` | `VARCHAR(255)` | True | False | - |
| `cancellation_source` | `VARCHAR(30)` | True | False | - |
| `cancelled_at` | `DATETIME` | True | False | - |
| `cancelled_by` | `INTEGER` | True | False | - |
| `payment_due_date` | `DATETIME` | True | False | - |
| `cancellation_policy_snapshot` | `TEXT` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `affiliate_id` references `affiliates.id`
- Column `agent_id` references `agents.id`
- Column `supplier_id` references `suppliers.id`
- Column `tour_calendar_id` references `tour_calendar.id`
- Column `tour_id` references `tours.id`
- Column `cancelled_by` references `users.id`
- Column `pricing_slab_id` references `tour_pricing.id`
- Column `group_discount_tier_id` references `tour_group_discount_tiers.id`
- Column `city_id` references `cities.id`
- Column `country_id` references `countries.id`
- Column `booked_by_user_id` references `users.id`
- Column `created_by` references `users.id`
- Column `customer_id` references `customers.id`
- Column `affiliate_attribution_id` references `affiliate_attributions.id`

### `cancellation_requests`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `booking_id` | `INTEGER` | False | False | - |
| `customer_id` | `INTEGER` | False | False | - |
| `reason` | `TEXT` | False | False | - |
| `status` | `VARCHAR(30)` | False | False | pending |
| `refund_percentage` | `NUMERIC(5, 2)` | False | False | 0 |
| `refund_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `refund_processed_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `admin_notes` | `TEXT` | True | False | - |
| `reviewed_by` | `INTEGER` | True | False | - |
| `reviewed_at` | `DATETIME` | True | False | - |
| `gateway_refund_id` | `VARCHAR(150)` | True | False | - |
| `refund_processed_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `booking_id` references `bookings.id`
- Column `customer_id` references `customers.id`
- Column `reviewed_by` references `users.id`

### `chat_embeddings`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `source_type` | `VARCHAR(20)` | False | False | - |
| `source_id` | `INTEGER` | False | False | - |
| `content_text` | `TEXT` | False | False | - |
| `content_hash` | `VARCHAR(64)` | False | False | - |
| `embedding` | `JSON` | False | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `chat_faqs`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `question` | `VARCHAR(500)` | False | False | - |
| `answer` | `TEXT` | False | False | - |
| `category` | `VARCHAR(100)` | False | False | general |
| `sort_order` | `INTEGER` | False | False | 0 |
| `is_active` | `BOOLEAN` | False | False | True |
| `is_public` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `chat_feedback`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `message_id` | `INTEGER` | False | False | - |
| `session_id` | `INTEGER` | False | False | - |
| `rating` | `INTEGER` | False | False | - |
| `comment` | `TEXT` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `message_id` references `chat_messages.id`
- Column `session_id` references `chat_sessions.id`

### `chat_messages`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `session_id` | `INTEGER` | False | False | - |
| `role` | `VARCHAR(20)` | False | False | - |
| `content` | `TEXT` | False | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `session_id` references `chat_sessions.id`

### `chat_sessions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `session_key` | `VARCHAR(64)` | False | False | - |
| `user_name` | `VARCHAR(120)` | False | False |  |
| `user_email` | `VARCHAR(255)` | False | False |  |
| `created_at` | `DATETIME` | True | False | - |

### `checkout_sessions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `session_key` | `VARCHAR(64)` | False | False | - |
| `user_id` | `INTEGER` | True | False | - |
| `customer_id` | `INTEGER` | True | False | - |
| `tour_id` | `INTEGER` | True | False | - |
| `tour_calendar_id` | `INTEGER` | True | False | - |
| `step` | `VARCHAR(50)` | False | False | tour_selection |
| `status` | `VARCHAR(30)` | False | False | active |
| `data` | `JSON` | True | False | - |
| `booking_id` | `INTEGER` | True | False | - |
| `expires_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `customer_id` references `customers.id`
- Column `user_id` references `users.id`
- Column `tour_id` references `tours.id`
- Column `booking_id` references `bookings.id`
- Column `tour_calendar_id` references `tour_calendar.id`

### `cities`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `country_id` | `INTEGER` | False | False | - |
| `state_id` | `INTEGER` | True | False | - |
| `city_name` | `VARCHAR(120)` | False | False | - |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `state_id` references `states.id`
- Column `country_id` references `countries.id`

### `cms_blogs`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `title` | `VARCHAR(200)` | False | False | - |
| `slug` | `VARCHAR(220)` | False | False | - |
| `excerpt` | `TEXT` | True | False | - |
| `content` | `TEXT` | True | False | - |
| `featured_image` | `VARCHAR(255)` | True | False | - |
| `banner_title` | `VARCHAR(200)` | True | False | - |
| `banner_alt` | `VARCHAR(300)` | True | False | - |
| `author` | `VARCHAR(120)` | True | False | - |
| `tags` | `JSON` | True | False | - |
| `faqs` | `JSON` | True | False | - |
| `seo_title` | `VARCHAR(200)` | True | False | - |
| `seo_description` | `VARCHAR(400)` | True | False | - |
| `status` | `VARCHAR(20)` | False | False | draft |
| `published_at` | `DATETIME` | True | False | - |
| `scheduled_at` | `DATETIME` | True | False | - |
| `created_by` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `created_by` references `users.id`

### `cms_country_pages`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `country_id` | `INTEGER` | False | False | - |
| `hero_title` | `VARCHAR(200)` | True | False | - |
| `hero_description` | `TEXT` | True | False | - |
| `hero_image` | `VARCHAR(255)` | True | False | - |
| `showcase_title` | `VARCHAR(200)` | True | False | - |
| `showcase_description` | `TEXT` | True | False | - |
| `showcase_image` | `VARCHAR(255)` | True | False | - |
| `seo_title` | `VARCHAR(200)` | True | False | - |
| `seo_description` | `VARCHAR(400)` | True | False | - |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `country_id` references `countries.id`

### `cms_customer_reviews`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `reviewer_name` | `VARCHAR(120)` | False | False | - |
| `reviewer_image` | `VARCHAR(255)` | True | False | - |
| `rating` | `FLOAT` | False | False | 5 |
| `review_text` | `TEXT` | False | False | - |
| `tour_name` | `VARCHAR(200)` | True | False | - |
| `country` | `VARCHAR(100)` | True | False | - |
| `sort_order` | `INTEGER` | False | False | 0 |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `cms_external_links`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `label` | `VARCHAR(120)` | False | False | - |
| `url` | `VARCHAR(500)` | False | False | - |
| `open_in_new_tab` | `BOOLEAN` | False | False | True |
| `location` | `VARCHAR(50)` | False | False | footer |
| `sort_order` | `INTEGER` | False | False | 0 |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `cms_favourite_countries`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `country_id` | `INTEGER` | True | False | - |
| `title` | `VARCHAR(200)` | False | False | - |
| `snippet` | `TEXT` | True | False | - |
| `image` | `VARCHAR(255)` | True | False | - |
| `href` | `VARCHAR(500)` | True | False | - |
| `sort_order` | `INTEGER` | False | False | 0 |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `country_id` references `countries.id`

### `cms_footer_links`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `section_id` | `INTEGER` | False | False | - |
| `label` | `VARCHAR(120)` | False | False | - |
| `url` | `VARCHAR(500)` | False | False | - |
| `open_in_new_tab` | `BOOLEAN` | False | False | False |
| `sort_order` | `INTEGER` | False | False | 0 |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `section_id` references `cms_footer_sections.id`

### `cms_footer_sections`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `title` | `VARCHAR(120)` | False | False | - |
| `sort_order` | `INTEGER` | False | False | 0 |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `cms_handpicked_tours`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `sort_order` | `INTEGER` | False | False | 0 |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `cms_help_centre`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `category` | `VARCHAR(100)` | False | False | - |
| `question` | `TEXT` | False | False | - |
| `answer` | `TEXT` | False | False | - |
| `sort_order` | `INTEGER` | False | False | 0 |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `cms_homepage_banners`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `title` | `VARCHAR(200)` | False | False | - |
| `subtitle` | `VARCHAR(400)` | True | False | - |
| `image` | `VARCHAR(255)` | True | False | - |
| `video` | `VARCHAR(255)` | True | False | - |
| `cta_text` | `VARCHAR(100)` | True | False | - |
| `cta_url` | `VARCHAR(500)` | True | False | - |
| `sort_order` | `INTEGER` | False | False | 0 |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `cms_homepage_content_blocks`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `key` | `VARCHAR(60)` | False | False | - |
| `data` | `JSON` | False | False | <function dict at 0x000001A117F57ED0> |
| `version` | `INTEGER` | False | False | 1 |
| `updated_at` | `DATETIME` | True | False | - |

### `cms_pages`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `title` | `VARCHAR(200)` | False | False | - |
| `slug` | `VARCHAR(220)` | False | False | - |
| `content` | `TEXT` | True | False | - |
| `sections` | `JSON` | True | False | - |
| `seo_title` | `VARCHAR(200)` | True | False | - |
| `seo_description` | `VARCHAR(400)` | True | False | - |
| `status` | `VARCHAR(20)` | False | False | draft |
| `footer_section_id` | `INTEGER` | True | False | - |
| `sort_order` | `INTEGER` | False | False | 0 |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `footer_section_id` references `cms_footer_sections.id`

### `cms_policies`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `slug` | `VARCHAR(80)` | False | False | - |
| `title` | `VARCHAR(200)` | False | False | - |
| `content` | `TEXT` | False | False | - |
| `last_updated` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `cms_popular_destinations`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `country_id` | `INTEGER` | True | False | - |
| `city_id` | `INTEGER` | True | False | - |
| `title` | `VARCHAR(200)` | False | False | - |
| `image` | `VARCHAR(255)` | True | False | - |
| `description` | `TEXT` | True | False | - |
| `href` | `VARCHAR(500)` | True | False | - |
| `rating` | `FLOAT` | True | False | - |
| `package_count` | `INTEGER` | True | False | - |
| `sort_order` | `INTEGER` | False | False | 0 |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `country_id` references `countries.id`
- Column `city_id` references `cities.id`

### `cms_popular_tours`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `sort_order` | `INTEGER` | False | False | 0 |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `cms_promotional_popups`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `title` | `VARCHAR(200)` | False | False | - |
| `content` | `TEXT` | True | False | - |
| `image` | `VARCHAR(255)` | True | False | - |
| `cta_text` | `VARCHAR(100)` | True | False | - |
| `cta_url` | `VARCHAR(500)` | True | False | - |
| `display_after_seconds` | `INTEGER` | False | False | 3 |
| `display_frequency` | `VARCHAR(20)` | False | False | once |
| `is_active` | `BOOLEAN` | False | False | False |
| `valid_from` | `DATETIME` | True | False | - |
| `valid_until` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `cms_sitemap_entries`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `url` | `VARCHAR(500)` | False | False | - |
| `change_frequency` | `VARCHAR(20)` | False | False | weekly |
| `priority` | `VARCHAR(5)` | False | False | 0.5 |
| `last_modified` | `DATETIME` | True | False | - |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `cms_tours_on_deals`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `deal_label` | `VARCHAR(100)` | True | False | - |
| `discount_percentage` | `INTEGER` | False | False | 0 |
| `valid_until` | `DATETIME` | True | False | - |
| `sort_order` | `INTEGER` | False | False | 0 |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `contact_messages`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `name` | `VARCHAR(150)` | False | False | - |
| `email` | `VARCHAR(255)` | False | False | - |
| `phone` | `VARCHAR(30)` | True | False | - |
| `audience` | `VARCHAR(20)` | False | False | public |
| `enquiry_type` | `VARCHAR(50)` | False | False | General enquiry |
| `subject` | `VARCHAR(200)` | False | False | - |
| `message` | `TEXT` | False | False | - |
| `is_replied` | `BOOLEAN` | False | False | False |
| `created_at` | `DATETIME` | True | False | - |

### `conversations`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `participant_type` | `VARCHAR(20)` | False | False | - |
| `participant_user_id` | `INTEGER` | False | False | - |
| `status` | `VARCHAR(20)` | False | False | open |
| `last_message_at` | `DATETIME` | True | False | - |
| `last_message_preview` | `VARCHAR(300)` | True | False | - |
| `admin_unread_count` | `INTEGER` | False | False | 0 |
| `participant_unread_count` | `INTEGER` | False | False | 0 |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `participant_user_id` references `users.id`

### `countries`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `country_name` | `VARCHAR(120)` | False | False | - |
| `slug` | `VARCHAR(150)` | False | False | - |
| `country_code` | `VARCHAR(10)` | False | False | - |
| `phone_code` | `VARCHAR(10)` | False | False |  |
| `currency_code` | `VARCHAR(10)` | False | False |  |
| `flag_emoji` | `VARCHAR(16)` | False | False |  |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `currencies`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `name` | `VARCHAR(120)` | False | False | - |
| `code` | `VARCHAR(10)` | False | False | - |
| `symbol` | `VARCHAR(10)` | False | False | - |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `customer_cancellation_requests`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `customer_id` | `INTEGER` | False | False | - |
| `booking_id` | `INTEGER` | False | False | - |
| `reason` | `TEXT` | False | False | - |
| `status` | `VARCHAR(30)` | False | False | requested |
| `admin_notes` | `TEXT` | True | False | - |
| `reviewed_by` | `INTEGER` | True | False | - |
| `reviewed_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `reviewed_by` references `users.id`
- Column `booking_id` references `bookings.id`
- Column `customer_id` references `customers.id`

### `customer_communications`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `customer_id` | `INTEGER` | True | False | - |
| `booking_id` | `INTEGER` | True | False | - |
| `subject` | `VARCHAR(150)` | False | False | - |
| `message` | `TEXT` | False | False | - |
| `sent_by_user_id` | `INTEGER` | True | False | - |
| `sent_to_email` | `VARCHAR(150)` | False | False | admin |
| `message_type` | `VARCHAR(30)` | False | False | admin_message |
| `email_status` | `VARCHAR(20)` | False | False | pending |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `sent_by_user_id` references `users.id`
- Column `customer_id` references `customers.id`
- Column `booking_id` references `bookings.id`

### `customer_saved_travellers`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `customer_id` | `INTEGER` | False | False | - |
| `traveller_name` | `VARCHAR(150)` | False | False | - |
| `email` | `VARCHAR(150)` | False | False |  |
| `phone` | `VARCHAR(50)` | False | False |  |
| `traveller_type` | `VARCHAR(20)` | False | False | adult |
| `age` | `INTEGER` | True | False | - |
| `gender` | `VARCHAR(30)` | True | False | - |
| `passport_number` | `VARCHAR(100)` | True | False | - |
| `allergies` | `TEXT` | True | False | - |
| `special_notes` | `TEXT` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `customer_id` references `customers.id`

### `customer_wishlist_items`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `user_id` | `INTEGER` | False | False | - |
| `tour_id` | `INTEGER` | False | False | - |
| `created_at` | `DATETIME` | False | False | - |
| `last_reminder_sent_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`
- Column `user_id` references `users.id`

### `customers`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `user_id` | `INTEGER` | True | False | - |
| `customer_code` | `VARCHAR(30)` | True | False | - |
| `customer_type` | `VARCHAR(20)` | False | False | registered |
| `agent_id` | `INTEGER` | True | False | - |
| `first_name` | `VARCHAR(75)` | False | False |  |
| `last_name` | `VARCHAR(75)` | False | False |  |
| `full_name` | `VARCHAR(150)` | False | False | - |
| `email` | `VARCHAR(150)` | False | False | - |
| `phone_country_code` | `VARCHAR(10)` | False | False |  |
| `phone` | `VARCHAR(30)` | False | False |  |
| `country_id` | `INTEGER` | True | False | - |
| `city_id` | `INTEGER` | True | False | - |
| `date_of_birth` | `DATETIME` | True | False | - |
| `gender` | `VARCHAR(30)` | True | False | - |
| `nationality` | `VARCHAR(100)` | False | False |  |
| `passport_number` | `VARCHAR(100)` | False | False |  |
| `passport_expiry` | `VARCHAR(40)` | False | False |  |
| `frequent_flyer` | `VARCHAR(100)` | False | False |  |
| `preferred_airline` | `VARCHAR(100)` | False | False |  |
| `emergency_name` | `VARCHAR(150)` | False | False |  |
| `emergency_relation` | `VARCHAR(100)` | False | False |  |
| `emergency_phone` | `VARCHAR(30)` | False | False |  |
| `emergency_email` | `VARCHAR(150)` | False | False |  |
| `address_line_1` | `VARCHAR(255)` | False | False |  |
| `address_line_2` | `VARCHAR(255)` | False | False |  |
| `postal_code` | `VARCHAR(20)` | False | False |  |
| `address` | `VARCHAR(255)` | False | False |  |
| `profile_image` | `VARCHAR(255)` | False | False |  |
| `country` | `VARCHAR(100)` | False | False |  |
| `state` | `VARCHAR(100)` | False | False |  |
| `city` | `VARCHAR(100)` | False | False |  |
| `pincode` | `VARCHAR(20)` | False | False |  |
| `status` | `VARCHAR(20)` | False | False | active |
| `email_verified` | `BOOLEAN` | False | False | False |
| `phone_verified` | `BOOLEAN` | False | False | False |
| `is_blocked` | `BOOLEAN` | False | False | False |
| `blocked_reason` | `VARCHAR(255)` | True | False | - |
| `blocked_at` | `DATETIME` | True | False | - |
| `blocked_by` | `INTEGER` | True | False | - |
| `total_bookings` | `INTEGER` | False | False | 0 |
| `completed_bookings` | `INTEGER` | False | False | 0 |
| `cancelled_bookings` | `INTEGER` | False | False | 0 |
| `upcoming_bookings` | `INTEGER` | False | False | 0 |
| `total_amount_paid` | `NUMERIC(12, 2)` | False | False | 0 |
| `total_amount_pending` | `NUMERIC(12, 2)` | False | False | 0 |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `user_id` references `users.id`
- Column `city_id` references `cities.id`
- Column `blocked_by` references `users.id`
- Column `country_id` references `countries.id`
- Column `agent_id` references `agents.id`

### `email_logs`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `recipient_email` | `VARCHAR(180)` | False | False | - |
| `subject` | `VARCHAR(255)` | False | False | - |
| `template_key` | `VARCHAR(100)` | True | False | - |
| `entity_type` | `VARCHAR(60)` | True | False | - |
| `entity_id` | `INTEGER` | True | False | - |
| `status` | `VARCHAR(30)` | False | False | pending |
| `error_message` | `TEXT` | True | False | - |
| `sent_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |

### `email_templates`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `key` | `VARCHAR(100)` | False | False | - |
| `name` | `VARCHAR(150)` | False | False | - |
| `subject` | `VARCHAR(200)` | False | False | - |
| `body` | `TEXT` | False | False | - |
| `is_active` | `BOOLEAN` | True | False | True |
| `updated_at` | `DATETIME` | True | False | - |

### `external_affiliate_clicks`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `provider` | `VARCHAR(40)` | False | False | - |
| `product_code` | `VARCHAR(80)` | False | False | - |
| `product_title` | `VARCHAR(255)` | True | False | - |
| `provider_destination_id` | `VARCHAR(40)` | True | False | - |
| `tourvaa_country_id` | `INTEGER` | True | False | - |
| `tourvaa_city_id` | `INTEGER` | True | False | - |
| `user_id` | `INTEGER` | True | False | - |
| `agent_id` | `INTEGER` | True | False | - |
| `session_id` | `VARCHAR(64)` | True | False | - |
| `campaign` | `VARCHAR(80)` | True | False | - |
| `source_page` | `VARCHAR(40)` | True | False | - |
| `page_path` | `VARCHAR(255)` | True | False | - |
| `external_url` | `TEXT` | True | False | - |
| `external_url_hash` | `VARCHAR(64)` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tourvaa_country_id` references `countries.id`
- Column `agent_id` references `agents.id`
- Column `tourvaa_city_id` references `cities.id`
- Column `user_id` references `users.id`

### `external_destination_mappings`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `provider` | `VARCHAR(40)` | False | False | - |
| `provider_destination_id` | `VARCHAR(40)` | False | False | - |
| `provider_destination_name` | `VARCHAR(255)` | False | False | - |
| `provider_destination_type` | `VARCHAR(40)` | True | False | - |
| `provider_parent_destination_id` | `VARCHAR(40)` | True | False | - |
| `provider_default_currency` | `VARCHAR(3)` | True | False | - |
| `provider_destination_url` | `TEXT` | True | False | - |
| `slug` | `VARCHAR(191)` | False | False | - |
| `tourvaa_country_id` | `INTEGER` | True | False | - |
| `tourvaa_state_id` | `INTEGER` | True | False | - |
| `tourvaa_city_id` | `INTEGER` | True | False | - |
| `mapping_source` | `VARCHAR(10)` | True | False | - |
| `is_active` | `BOOLEAN` | False | False | True |
| `last_synced_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tourvaa_city_id` references `cities.id`
- Column `tourvaa_state_id` references `states.id`
- Column `tourvaa_country_id` references `countries.id`

### `external_providers`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `code` | `VARCHAR(40)` | False | False | - |
| `name` | `VARCHAR(100)` | False | False | - |
| `public_category` | `VARCHAR(120)` | False | False | Day Tours & Experiences |
| `show_on_homepage` | `BOOLEAN` | False | False | True |
| `show_on_destination_pages` | `BOOLEAN` | False | False | True |
| `show_on_itinerary` | `BOOLEAN` | False | False | True |
| `show_in_search` | `BOOLEAN` | False | False | True |
| `last_connection_status` | `VARCHAR(20)` | True | False | - |
| `last_connection_message` | `VARCHAR(255)` | True | False | - |
| `last_connection_at` | `DATETIME` | True | False | - |
| `last_destination_sync_at` | `DATETIME` | True | False | - |
| `last_destination_sync_status` | `VARCHAR(20)` | True | False | - |
| `last_destination_sync_count` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `invoice_items`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `invoice_id` | `INTEGER` | False | False | - |
| `item_type` | `VARCHAR(40)` | False | False | booking |
| `description` | `VARCHAR(255)` | False | False | - |
| `quantity` | `INTEGER` | False | False | 1 |
| `unit_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `tax_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `total_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `invoice_id` references `invoices.id`

### `invoices`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `invoice_number` | `VARCHAR(40)` | True | False | - |
| `booking_id` | `INTEGER` | False | False | - |
| `payment_id` | `INTEGER` | True | False | - |
| `customer_id` | `INTEGER` | True | False | - |
| `invoice_type` | `VARCHAR(30)` | False | False | tax_invoice |
| `recipient_type` | `VARCHAR(20)` | False | False | customer |
| `document_snapshot` | `JSON` | True | False | - |
| `status` | `VARCHAR(30)` | False | False | generated |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `subtotal_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `gst_rate` | `NUMERIC(5, 4)` | False | False | 0.18 |
| `gst_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `total_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `amount_paid` | `NUMERIC(12, 2)` | False | False | 0 |
| `amount_due` | `NUMERIC(12, 2)` | False | False | 0 |
| `balance_due_date` | `DATETIME` | True | False | - |
| `balance_reminder_stage` | `VARCHAR(20)` | True | False | - |
| `last_balance_reminder_at` | `DATETIME` | True | False | - |
| `pdf_path` | `VARCHAR(255)` | True | False | - |
| `emailed_at` | `DATETIME` | True | False | - |
| `created_by` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `booking_id` references `bookings.id`
- Column `payment_id` references `payments.id`
- Column `created_by` references `users.id`
- Column `customer_id` references `customers.id`

### `login_history`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `user_id` | `INTEGER` | True | False | - |
| `email` | `VARCHAR(150)` | False | False | - |
| `status` | `VARCHAR(30)` | False | False | - |
| `failure_reason` | `VARCHAR(255)` | True | False | - |
| `client_type` | `VARCHAR(30)` | False | False | web |
| `device_id` | `VARCHAR(120)` | True | False | - |
| `device_name` | `VARCHAR(180)` | True | False | - |
| `ip_address` | `VARCHAR(100)` | True | False | - |
| `user_agent` | `VARCHAR(255)` | True | False | - |
| `session_id` | `VARCHAR(120)` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `user_id` references `users.id`

### `message_replies`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `communication_id` | `INTEGER` | False | False | - |
| `sender_user_id` | `INTEGER` | True | False | - |
| `sender_type` | `VARCHAR(30)` | False | False | admin |
| `message` | `TEXT` | False | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `sender_user_id` references `users.id`
- Column `communication_id` references `booking_communications.id`

### `messages`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `conversation_id` | `INTEGER` | False | False | - |
| `sender_user_id` | `INTEGER` | True | False | - |
| `sender_role` | `VARCHAR(20)` | False | False | - |
| `body` | `TEXT` | False | False | - |
| `is_deleted` | `BOOLEAN` | False | False | False |
| `deleted_at` | `DATETIME` | True | False | - |
| `delivered_at` | `DATETIME` | True | False | - |
| `read_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `sender_user_id` references `users.id`
- Column `conversation_id` references `conversations.id`

### `newsletter_subscribers`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `email` | `VARCHAR(255)` | False | False | - |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |

### `notification_deliveries`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `event_type` | `VARCHAR(100)` | False | False | - |
| `entity_type` | `VARCHAR(60)` | False | False | - |
| `entity_id` | `INTEGER` | False | False | - |
| `recipient_type` | `VARCHAR(40)` | False | False | - |
| `recipient_email` | `VARCHAR(180)` | False | False | - |
| `template_key` | `VARCHAR(100)` | False | False | - |
| `subject` | `VARCHAR(255)` | True | False | - |
| `payload_json` | `JSON` | True | False | - |
| `status` | `VARCHAR(30)` | False | False | pending |
| `attempt_count` | `INTEGER` | False | False | 0 |
| `next_attempt_at` | `DATETIME` | True | False | - |
| `lease_token` | `VARCHAR(64)` | True | False | - |
| `lease_expires_at` | `DATETIME` | True | False | - |
| `error_message` | `TEXT` | True | False | - |
| `idempotency_key` | `VARCHAR(255)` | False | False | - |
| `sent_at` | `DATETIME` | True | False | - |
| `smtp_accepted_at` | `DATETIME` | True | False | - |
| `exhausted_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `notification_logs`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `notification_id` | `INTEGER` | True | False | - |
| `channel` | `VARCHAR(30)` | False | False | - |
| `status` | `VARCHAR(30)` | False | False | - |
| `response` | `TEXT` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `notification_id` references `notifications.id`

### `notifications`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `user_id` | `INTEGER` | True | False | - |
| `notification_type` | `VARCHAR(60)` | False | False | - |
| `title` | `VARCHAR(180)` | False | False | - |
| `message` | `TEXT` | False | False | - |
| `channel` | `VARCHAR(30)` | False | False | in_app |
| `status` | `VARCHAR(30)` | False | False | pending |
| `is_read` | `INTEGER` | False | False | 0 |
| `entity_type` | `VARCHAR(60)` | True | False | - |
| `entity_id` | `INTEGER` | True | False | - |
| `notification_id` | `VARCHAR(100)` | True | False | - |
| `metadata_json` | `JSON` | True | False | - |
| `event_key` | `VARCHAR(100)` | True | False | - |
| `event_version` | `VARCHAR(100)` | True | False | - |
| `idempotency_key` | `VARCHAR(255)` | True | False | - |
| `sent_at` | `DATETIME` | True | False | - |
| `read_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `user_id` references `users.id`

### `payment_holds`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `payment_id` | `INTEGER` | False | False | - |
| `booking_id` | `INTEGER` | False | False | - |
| `hold_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `captured_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `released_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `status` | `VARCHAR(30)` | False | False | active |
| `expires_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `payment_id` references `payments.id`
- Column `booking_id` references `bookings.id`

### `payment_settings`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `provider_name` | `VARCHAR(100)` | False | False | - |
| `is_enabled` | `BOOLEAN` | False | False | False |
| `public_key` | `TEXT` | True | False | - |
| `secret_key` | `TEXT` | True | False | - |
| `webhook_id` | `VARCHAR(150)` | True | False | - |
| `sandbox_client_id` | `TEXT` | True | False | - |
| `sandbox_secret` | `TEXT` | True | False | - |
| `live_client_id` | `TEXT` | True | False | - |
| `live_secret` | `TEXT` | True | False | - |
| `surcharge_percentage` | `VARCHAR(20)` | False | False | 0 |
| `mode` | `VARCHAR(20)` | False | False | test |
| `last_test_status` | `VARCHAR(20)` | True | False | - |
| `last_test_at` | `DATETIME` | True | False | - |
| `last_test_error` | `TEXT` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `payment_transactions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `payment_id` | `INTEGER` | False | False | - |
| `booking_id` | `INTEGER` | False | False | - |
| `transaction_type` | `VARCHAR(30)` | False | False | - |
| `amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `status` | `VARCHAR(30)` | False | False | success |
| `gateway_reference` | `VARCHAR(150)` | True | False | - |
| `metadata_json` | `JSON` | True | False | - |
| `created_by` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `booking_id` references `bookings.id`
- Column `payment_id` references `payments.id`
- Column `created_by` references `users.id`

### `payments`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `payment_code` | `VARCHAR(30)` | True | False | - |
| `booking_id` | `INTEGER` | False | False | - |
| `customer_id` | `INTEGER` | True | False | - |
| `created_by` | `INTEGER` | True | False | - |
| `payment_method` | `VARCHAR(30)` | False | False | card |
| `payment_type` | `VARCHAR(30)` | False | False | full |
| `gateway` | `VARCHAR(50)` | False | False | manual |
| `gateway_payment_id` | `VARCHAR(150)` | True | False | - |
| `gateway_order_id` | `VARCHAR(150)` | True | False | - |
| `idempotency_key` | `VARCHAR(150)` | True | False | - |
| `total_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `authorized_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `captured_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `paid_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `pending_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `gst_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `surcharge_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `refunded_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `payment_status` | `VARCHAR(30)` | False | False | pending |
| `transaction_id` | `VARCHAR(100)` | True | False | - |
| `payment_date` | `VARCHAR(30)` | True | False | - |
| `notes` | `TEXT` | True | False | - |
| `failure_reason` | `VARCHAR(255)` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `customer_id` references `customers.id`
- Column `created_by` references `users.id`
- Column `booking_id` references `bookings.id`

### `permissions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `name` | `VARCHAR(150)` | False | False | - |
| `slug` | `VARCHAR(150)` | False | False | - |
| `module` | `VARCHAR(100)` | False | False | - |
| `action` | `VARCHAR(20)` | False | False | get |
| `is_active` | `BOOLEAN` | True | False | True |
| `is_system` | `BOOLEAN` | False | False | False |
| `created_at` | `DATETIME` | True | False | - |

### `push_delivery_logs`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `notification_id` | `INTEGER` | True | False | - |
| `subscription_id` | `INTEGER` | True | False | - |
| `event_key` | `VARCHAR(100)` | True | False | - |
| `recipient_user_id` | `INTEGER` | True | False | - |
| `provider` | `VARCHAR(30)` | False | False | web_push |
| `status` | `VARCHAR(30)` | False | False | pending |
| `attempt_count` | `INTEGER` | False | False | 0 |
| `error_message` | `TEXT` | True | False | - |
| `sent_at` | `DATETIME` | True | False | - |
| `failed_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `recipient_user_id` references `users.id`
- Column `notification_id` references `notifications.id`
- Column `subscription_id` references `push_subscriptions.id`

### `push_subscriptions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `user_id` | `INTEGER` | True | False | - |
| `endpoint` | `TEXT` | False | False | - |
| `endpoint_hash` | `VARCHAR(64)` | False | False | - |
| `p256dh` | `VARCHAR(256)` | False | False | - |
| `auth` | `VARCHAR(255)` | False | False | - |
| `platform` | `VARCHAR(20)` | True | False | - |
| `device_type` | `VARCHAR(30)` | True | False | - |
| `is_active` | `INTEGER` | False | False | 1 |
| `last_used_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `user_id` references `users.id`

### `refund_rules`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | True | False | - |
| `days_before_tour_min` | `INTEGER` | False | False | - |
| `days_before_tour_max` | `INTEGER` | True | False | - |
| `refund_percentage` | `NUMERIC(5, 2)` | False | False | 0 |
| `description` | `VARCHAR(255)` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `report_schedules`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `report_type` | `VARCHAR(50)` | False | False | - |
| `cadence` | `VARCHAR(20)` | False | False | weekly |
| `recipient_emails` | `VARCHAR(1000)` | False | False | - |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_by` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `last_run_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `created_by` references `users.id`

### `role_permissions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `role_id` | `INTEGER` | False | False | - |
| `permission_id` | `INTEGER` | False | False | - |

**Foreign Keys:**
- Column `permission_id` references `permissions.id`
- Column `role_id` references `roles.id`

### `roles`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `name` | `VARCHAR(100)` | False | False | - |
| `slug` | `VARCHAR(100)` | False | False | - |
| `is_active` | `BOOLEAN` | True | False | True |
| `is_system` | `BOOLEAN` | False | False | False |
| `created_at` | `DATETIME` | True | False | - |

### `smtp_settings`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `is_enabled` | `BOOLEAN` | False | False | False |
| `host` | `VARCHAR(255)` | True | False | - |
| `port` | `INTEGER` | False | False | 465 |
| `username` | `VARCHAR(255)` | True | False | - |
| `password` | `TEXT` | True | False | - |
| `from_name` | `VARCHAR(150)` | False | False | Tourvaa |
| `from_email` | `VARCHAR(255)` | True | False | - |
| `reply_to` | `VARCHAR(255)` | True | False | - |
| `admin_notification_to` | `TEXT` | True | False | - |
| `admin_notification_cc` | `TEXT` | True | False | - |
| `admin_notification_bcc` | `TEXT` | True | False | - |
| `use_ssl` | `BOOLEAN` | False | False | True |
| `use_starttls` | `BOOLEAN` | False | False | False |
| `timeout_seconds` | `INTEGER` | False | False | 20 |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `states`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `country_id` | `INTEGER` | False | False | - |
| `state_name` | `VARCHAR(150)` | False | False | - |
| `state_code` | `VARCHAR(10)` | False | False |  |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `country_id` references `countries.id`

### `supplier_approval_history`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `supplier_id` | `INTEGER` | False | False | - |
| `from_status` | `VARCHAR(30)` | True | False | - |
| `to_status` | `VARCHAR(30)` | False | False | - |
| `notes` | `TEXT` | True | False | - |
| `changed_by` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | False | False | - |

**Foreign Keys:**
- Column `supplier_id` references `suppliers.id`
- Column `changed_by` references `users.id`

### `supplier_business_info`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `supplier_id` | `INTEGER` | False | False | - |
| `years_in_business` | `INTEGER` | False | False | 0 |
| `certificate_of_incorporation` | `VARCHAR(255)` | False | False |  |
| `monthly_customers_count` | `INTEGER` | False | False | 0 |
| `target_market` | `VARCHAR(255)` | False | False |  |
| `destinations_sold` | `TEXT` | False | False |  |
| `gst_tax_number` | `VARCHAR(100)` | False | False |  |
| `business_registration_number` | `VARCHAR(100)` | False | False |  |
| `trading_name` | `VARCHAR(150)` | False | False |  |
| `business_email` | `VARCHAR(150)` | False | False |  |
| `website_url` | `VARCHAR(255)` | False | False |  |
| `approval_status` | `VARCHAR(30)` | False | False | pending |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `supplier_id` references `suppliers.id`

### `supplier_contacts`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `supplier_id` | `INTEGER` | False | False | - |
| `contact_name` | `VARCHAR(150)` | False | False | - |
| `first_name` | `VARCHAR(75)` | False | False |  |
| `last_name` | `VARCHAR(75)` | False | False |  |
| `designation` | `VARCHAR(100)` | False | False |  |
| `phone` | `VARCHAR(30)` | False | False |  |
| `email` | `VARCHAR(150)` | False | False |  |
| `alternate_phone` | `VARCHAR(30)` | False | False |  |
| `preferred_contact_method` | `VARCHAR(20)` | False | False |  |
| `is_primary` | `BOOLEAN` | False | False | False |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `supplier_id` references `suppliers.id`

### `supplier_documents`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `supplier_id` | `INTEGER` | False | False | - |
| `document_type` | `VARCHAR(100)` | False | False | - |
| `document_name` | `VARCHAR(150)` | False | False | - |
| `file_path` | `VARCHAR(255)` | False | False | - |
| `file_size` | `INTEGER` | False | False | 0 |
| `mime_type` | `VARCHAR(100)` | False | False |  |
| `status` | `VARCHAR(20)` | False | False | pending |
| `rejection_reason` | `VARCHAR(255)` | True | False | - |
| `uploaded_at` | `DATETIME` | True | False | - |
| `reviewed_at` | `DATETIME` | True | False | - |
| `reviewed_by` | `INTEGER` | True | False | - |

**Foreign Keys:**
- Column `supplier_id` references `suppliers.id`
- Column `reviewed_by` references `users.id`

### `supplier_invoicing`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `supplier_id` | `INTEGER` | False | False | - |
| `contact_name` | `VARCHAR(150)` | False | False |  |
| `email` | `VARCHAR(150)` | False | False |  |
| `phone` | `VARCHAR(30)` | False | False |  |
| `preferred_payment_method` | `VARCHAR(30)` | False | False |  |
| `account_name` | `VARCHAR(150)` | False | False |  |
| `account_number` | `VARCHAR(100)` | False | False |  |
| `bank_name` | `VARCHAR(150)` | False | False |  |
| `bank_branch` | `VARCHAR(150)` | False | False |  |
| `swift_code` | `VARCHAR(50)` | False | False |  |
| `iban` | `VARCHAR(100)` | False | False |  |
| `bank_country_id` | `INTEGER` | True | False | - |
| `country_id` | `INTEGER` | True | False | - |
| `tax_number` | `VARCHAR(100)` | False | False |  |
| `billing_address` | `TEXT` | True | False | - |
| `billing_city` | `VARCHAR(100)` | False | False |  |
| `billing_state` | `VARCHAR(100)` | False | False |  |
| `billing_postal_code` | `VARCHAR(30)` | False | False |  |
| `bank_edit_requested_at` | `DATETIME` | True | False | - |
| `bank_edit_unlocked_at` | `DATETIME` | True | False | - |
| `bank_edit_unlocked_by` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `supplier_id` references `suppliers.id`
- Column `bank_edit_unlocked_by` references `users.id`
- Column `bank_country_id` references `countries.id`
- Column `country_id` references `countries.id`

### `supplier_ledgers`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `supplier_id` | `INTEGER` | False | False | - |
| `booking_id` | `INTEGER` | False | False | - |
| `gross_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `commission_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `commission_percentage` | `NUMERIC(5, 2)` | False | False | 0 |
| `net_payable` | `NUMERIC(12, 2)` | False | False | 0 |
| `amount_paid` | `NUMERIC(12, 2)` | False | False | 0 |
| `amount_pending` | `NUMERIC(12, 2)` | False | False | 0 |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `status` | `VARCHAR(30)` | False | False | pending |
| `notes` | `TEXT` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `supplier_id` references `suppliers.id`
- Column `booking_id` references `bookings.id`

### `supplier_payout_items`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `payout_id` | `INTEGER` | False | False | - |
| `ledger_id` | `INTEGER` | False | False | - |
| `amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `payout_id` references `supplier_payouts.id`
- Column `ledger_id` references `supplier_ledgers.id`

### `supplier_payouts`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `payout_code` | `VARCHAR(30)` | True | False | - |
| `supplier_id` | `INTEGER` | False | False | - |
| `total_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `payment_method` | `VARCHAR(50)` | False | False | bank_transfer |
| `reference_number` | `VARCHAR(150)` | True | False | - |
| `status` | `VARCHAR(30)` | False | False | pending |
| `notes` | `TEXT` | True | False | - |
| `initiated_by` | `INTEGER` | True | False | - |
| `approved_by` | `INTEGER` | True | False | - |
| `paid_by` | `INTEGER` | True | False | - |
| `paid_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `paid_by` references `users.id`
- Column `initiated_by` references `users.id`
- Column `approved_by` references `users.id`
- Column `supplier_id` references `suppliers.id`

### `supplier_vehicles`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `supplier_id` | `INTEGER` | False | False | - |
| `make` | `VARCHAR(100)` | False | False |  |
| `model` | `VARCHAR(100)` | False | False |  |
| `vehicle_type` | `VARCHAR(75)` | False | False |  |
| `registration_number` | `VARCHAR(100)` | False | False |  |
| `year` | `INTEGER` | True | False | - |
| `capacity` | `INTEGER` | True | False | - |
| `fitness_certificate` | `VARCHAR(255)` | False | False |  |
| `insurance_document` | `VARCHAR(255)` | False | False |  |
| `vehicle_photos` | `TEXT` | False | False |  |
| `approval_status` | `VARCHAR(30)` | False | False | pending |
| `rejection_reason` | `VARCHAR(255)` | True | False | - |
| `reviewed_at` | `DATETIME` | True | False | - |
| `reviewed_by` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `reviewed_by` references `users.id`
- Column `supplier_id` references `suppliers.id`

### `suppliers`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `user_id` | `INTEGER` | True | False | - |
| `supplier_code` | `VARCHAR(30)` | True | False | - |
| `supplier_name` | `VARCHAR(150)` | False | False | - |
| `supplier_type` | `VARCHAR(75)` | False | False |  |
| `country_id` | `INTEGER` | True | False | - |
| `city_id` | `INTEGER` | True | False | - |
| `currency` | `VARCHAR(10)` | True | False | - |
| `years_in_operation` | `INTEGER` | False | False | 0 |
| `status` | `VARCHAR(20)` | False | False | inactive |
| `approval_status` | `VARCHAR(30)` | False | False | pending |
| `rejection_reason` | `VARCHAR(255)` | True | False | - |
| `admin_comments` | `TEXT` | True | False | - |
| `pending_requirements` | `TEXT` | True | False | - |
| `approved_at` | `DATETIME` | True | False | - |
| `approved_by` | `INTEGER` | True | False | - |
| `rejected_at` | `DATETIME` | True | False | - |
| `rejected_by` | `INTEGER` | True | False | - |
| `commission_percentage` | `NUMERIC(5, 2)` | True | False | - |
| `onboarding_completed_at` | `DATETIME` | True | False | - |
| `commission_accepted_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `rejected_by` references `users.id`
- Column `approved_by` references `users.id`
- Column `city_id` references `cities.id`
- Column `country_id` references `countries.id`
- Column `user_id` references `users.id`

### `tour_accommodation_extras`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `accommodation_name` | `VARCHAR(255)` | False | False | - |
| `description` | `TEXT` | True | False |  |
| `extra_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `price_type` | `VARCHAR(20)` | False | False | per_person |
| `image` | `VARCHAR(255)` | True | False |  |
| `category` | `VARCHAR(30)` | False | False | room_upgrade |
| `is_default` | `INTEGER` | False | False | 0 |
| `status` | `VARCHAR(20)` | False | False | active |
| `commissionable` | `BOOLEAN` | False | False | True |
| `supplier_cost` | `NUMERIC(12, 2)` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_availability_configs`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `availability_start_date` | `DATETIME` | True | False | - |
| `availability_end_date` | `DATETIME` | True | False | - |
| `min_advance_booking_days` | `INTEGER` | False | False | 0 |
| `agent_no_deposit_buffer_weeks` | `INTEGER` | False | False | 4 |
| `agent_reserve_deposit_percentage` | `FLOAT` | False | False | 30.0 |
| `frequency` | `VARCHAR(20)` | True | False | - |
| `frequency_week` | `INTEGER` | True | False | - |
| `frequency_weeks` | `JSON` | True | False | - |
| `frequency_days` | `JSON` | True | False | - |
| `seats_per_occurrence` | `INTEGER` | False | False | 0 |
| `last_end_date_reminder_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_calendar`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `tour_date` | `DATETIME` | False | False | - |
| `tour_date_day` | `DATE` | False | False | - |
| `start_date` | `DATETIME` | True | False | - |
| `end_date` | `DATETIME` | True | False | - |
| `available_seats` | `INTEGER` | False | False | 0 |
| `booked_seats` | `INTEGER` | False | False | 0 |
| `status` | `VARCHAR(20)` | False | False | available |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_categories`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `category_name` | `VARCHAR(120)` | False | False | - |
| `slug` | `VARCHAR(150)` | False | False | - |
| `description` | `TEXT` | False | False |  |
| `image` | `VARCHAR(255)` | False | False |  |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `tour_date_prices`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `price_date` | `DATE` | False | False | - |
| `adult_price` | `NUMERIC(12, 2)` | False | False | - |
| `child_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_discount_history`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `discount_id` | `INTEGER` | False | False | - |
| `version_number` | `INTEGER` | False | False | - |
| `change_type` | `VARCHAR(30)` | False | False | - |
| `discount_name` | `VARCHAR(255)` | False | False | - |
| `discount_type` | `VARCHAR(20)` | False | False | - |
| `discount_value` | `NUMERIC(12, 2)` | False | False | - |
| `start_date` | `DATETIME` | True | False | - |
| `end_date` | `DATETIME` | True | False | - |
| `reason` | `VARCHAR(500)` | True | False | - |
| `changed_by` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `changed_by` references `users.id`
- Column `discount_id` references `tour_discounts.id`

### `tour_discount_redemptions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `discount_id` | `INTEGER` | False | False | - |
| `booking_id` | `INTEGER` | False | False | - |
| `discount_amount` | `NUMERIC(12, 2)` | False | False | - |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `applied_at` | `DATETIME` | False | False | - |

**Foreign Keys:**
- Column `discount_id` references `tour_discounts.id`
- Column `booking_id` references `bookings.id`

### `tour_discounts`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | True | False | - |
| `category_id` | `INTEGER` | True | False | - |
| `country_id` | `INTEGER` | True | False | - |
| `discount_name` | `VARCHAR(255)` | False | False | - |
| `discount_code` | `VARCHAR(50)` | True | False | - |
| `discount_type` | `VARCHAR(20)` | False | False | - |
| `discount_value` | `NUMERIC(12, 2)` | False | False | - |
| `discount_scope` | `VARCHAR(20)` | False | False | tour |
| `start_date` | `DATETIME` | True | False | - |
| `end_date` | `DATETIME` | True | False | - |
| `usage_limit` | `INTEGER` | True | False | - |
| `used_count` | `INTEGER` | False | False | 0 |
| `minimum_booking_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `status` | `VARCHAR(20)` | False | False | active |
| `funded_by` | `VARCHAR(20)` | False | False | SUPPLIER |
| `show_on_website` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`
- Column `country_id` references `countries.id`
- Column `category_id` references `tour_categories.id`

### `tour_exclusions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `icon` | `VARCHAR(255)` | False | False |  |
| `title` | `VARCHAR(255)` | False | False | - |
| `description` | `TEXT` | True | False |  |
| `display_order` | `INTEGER` | False | False | 0 |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_extensions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `extension_tour_id` | `INTEGER` | False | False | - |
| `extension_title` | `VARCHAR(255)` | False | False |  |
| `extension_note` | `TEXT` | True | False |  |
| `extra_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `price_type` | `VARCHAR(20)` | False | False | per_booking |
| `category` | `VARCHAR(30)` | False | False | other |
| `display_order` | `INTEGER` | False | False | 0 |
| `status` | `VARCHAR(20)` | False | False | active |
| `commissionable` | `BOOLEAN` | False | False | True |
| `supplier_cost` | `NUMERIC(12, 2)` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`
- Column `extension_tour_id` references `tours.id`

### `tour_gallery_images`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `image_path` | `VARCHAR(255)` | False | False | - |
| `image_title` | `VARCHAR(255)` | False | False |  |
| `image_alt_text` | `VARCHAR(180)` | False | False |  |
| `image_caption` | `TEXT` | True | False |  |
| `image_type` | `VARCHAR(30)` | False | False | gallery |
| `display_order` | `INTEGER` | False | False | 0 |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_group_discount_tiers`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `min_pax` | `INTEGER` | False | False | - |
| `max_pax` | `INTEGER` | False | False | - |
| `discount_type` | `VARCHAR(20)` | False | False | - |
| `discount_value` | `NUMERIC(12, 2)` | False | False | - |
| `status` | `VARCHAR(20)` | False | False | active |
| `funded_by` | `VARCHAR(20)` | False | False | SUPPLIER |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_highlights`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `image` | `VARCHAR(255)` | False | False |  |
| `title` | `VARCHAR(255)` | False | False | - |
| `short_description` | `TEXT` | True | False |  |
| `display_order` | `INTEGER` | False | False | 0 |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_inclusions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `icon` | `VARCHAR(255)` | False | False |  |
| `title` | `VARCHAR(255)` | False | False | - |
| `description` | `TEXT` | True | False |  |
| `display_order` | `INTEGER` | False | False | 0 |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_itineraries`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `day_number` | `INTEGER` | False | False | - |
| `day_title` | `VARCHAR(255)` | False | False |  |
| `location_name` | `VARCHAR(255)` | False | False |  |
| `short_description` | `TEXT` | True | False |  |
| `long_description` | `TEXT` | True | False |  |
| `activities` | `TEXT` | True | False |  |
| `optional_activities` | `TEXT` | True | False |  |
| `accommodation` | `VARCHAR(255)` | True | False |  |
| `start_time` | `VARCHAR(20)` | True | False | - |
| `end_time` | `VARCHAR(20)` | True | False | - |
| `travel_distance` | `VARCHAR(100)` | True | False | - |
| `travel_duration` | `VARCHAR(100)` | True | False | - |
| `transport_type` | `VARCHAR(100)` | True | False | - |
| `meals_included` | `VARCHAR(150)` | True | False | - |
| `important_notes` | `TEXT` | True | False | - |
| `image` | `VARCHAR(255)` | False | False |  |
| `image_alt_text` | `VARCHAR(180)` | False | False |  |
| `images` | `TEXT` | True | False | [] |
| `display_order` | `INTEGER` | False | False | 0 |
| `status` | `VARCHAR(20)` | False | False | active |
| `day_type` | `VARCHAR(20)` | False | False | standard |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_optional_activities`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `activity_name` | `VARCHAR(255)` | False | False | - |
| `description` | `TEXT` | True | False |  |
| `price_per_person` | `NUMERIC(12, 2)` | False | False | 0 |
| `child_price_per_person` | `NUMERIC(12, 2)` | True | False | - |
| `infant_price_per_person` | `NUMERIC(12, 2)` | True | False | - |
| `pricing_mode` | `VARCHAR(20)` | False | False | flat |
| `image` | `VARCHAR(255)` | False | False |  |
| `category` | `VARCHAR(30)` | False | False | other |
| `status` | `VARCHAR(20)` | False | False | active |
| `commissionable` | `BOOLEAN` | False | False | True |
| `supplier_cost` | `NUMERIC(12, 2)` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_overviews`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `duration_text` | `VARCHAR(100)` | False | False |  |
| `start_location` | `VARCHAR(150)` | False | False |  |
| `end_location` | `VARCHAR(150)` | False | False |  |
| `group_size` | `VARCHAR(100)` | False | False |  |
| `tour_type` | `VARCHAR(100)` | False | False |  |
| `vehicle_style` | `VARCHAR(100)` | False | False |  |
| `guide_style` | `VARCHAR(50)` | False | False |  |
| `physical_rating` | `VARCHAR(20)` | False | False | easy |
| `overview_icon_data` | `JSON` | True | False | - |
| `why_choose_this_tour` | `TEXT` | True | False | - |
| `ideal_for` | `TEXT` | True | False | - |
| `best_season` | `VARCHAR(150)` | True | False | - |
| `tour_pace` | `VARCHAR(50)` | True | False | - |
| `transportation_summary` | `TEXT` | True | False | - |
| `accommodation_summary` | `TEXT` | True | False | - |
| `meal_summary` | `TEXT` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_pricing`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `passenger_from` | `INTEGER` | False | False | - |
| `passenger_to` | `INTEGER` | False | False | - |
| `adult_price` | `NUMERIC(12, 2)` | False | False | - |
| `child_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `supplier_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `final_price` | `NUMERIC(12, 2)` | False | False | - |
| `supplier_final_adult_price` | `NUMERIC(12, 2)` | True | False | - |
| `supplier_final_child_price` | `NUMERIC(12, 2)` | True | False | - |
| `commission_percentage` | `NUMERIC(5, 2)` | True | False | - |
| `admin_markup_type` | `VARCHAR(20)` | False | False | percentage |
| `admin_markup_value` | `NUMERIC(12, 2)` | True | False | - |
| `storefront_adult_price` | `NUMERIC(12, 2)` | True | False | - |
| `storefront_child_price` | `NUMERIC(12, 2)` | True | False | - |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_review_comments`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `version_id` | `INTEGER` | True | False | - |
| `section` | `VARCHAR(50)` | False | False | - |
| `field_name` | `VARCHAR(100)` | True | False | - |
| `comment` | `TEXT` | False | False | - |
| `severity` | `VARCHAR(20)` | False | False | minor |
| `status` | `VARCHAR(20)` | False | False | open |
| `created_by` | `INTEGER` | True | False | - |
| `resolved_by` | `INTEGER` | True | False | - |
| `resolved_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`
- Column `resolved_by` references `users.id`
- Column `version_id` references `tour_versions.id`
- Column `created_by` references `users.id`

### `tour_reviews`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `booking_id` | `INTEGER` | False | False | - |
| `customer_id` | `INTEGER` | False | False | - |
| `tour_id` | `INTEGER` | False | False | - |
| `rating` | `INTEGER` | False | False | - |
| `review_text` | `TEXT` | True | False | - |
| `status` | `VARCHAR(30)` | False | False | pending |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `customer_id` references `customers.id`
- Column `booking_id` references `bookings.id`
- Column `tour_id` references `tours.id`

### `tour_similar_tours`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `similar_tour_id` | `INTEGER` | False | False | - |
| `display_order` | `INTEGER` | False | False | 0 |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`
- Column `similar_tour_id` references `tours.id`

### `tour_subcategories`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `category_id` | `INTEGER` | False | False | - |
| `subcategory_name` | `VARCHAR(120)` | False | False | - |
| `slug` | `VARCHAR(150)` | False | False | - |
| `description` | `TEXT` | False | False |  |
| `image` | `VARCHAR(255)` | False | False |  |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `category_id` references `tour_categories.id`

### `tour_subcategory_map`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `subcategory_id` | `INTEGER` | False | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`
- Column `subcategory_id` references `tour_subcategories.id`

### `tour_unavailable_dates`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `unavailable_date` | `DATETIME` | False | False | - |
| `reason` | `TEXT` | True | False |  |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_versions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `version_number` | `INTEGER` | False | False | 1 |
| `snapshot` | `JSON` | False | False | - |
| `status` | `VARCHAR(30)` | False | False | pending_approval |
| `change_kind` | `VARCHAR(30)` | False | False | pending_approval |
| `submitted_by` | `INTEGER` | True | False | - |
| `reviewed_by` | `INTEGER` | True | False | - |
| `rejection_reason` | `TEXT` | True | False | - |
| `submitted_at` | `DATETIME` | True | False | - |
| `reviewed_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`
- Column `reviewed_by` references `users.id`
- Column `submitted_by` references `users.id`

### `tours`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_code` | `VARCHAR(30)` | True | False | - |
| `supplier_id` | `INTEGER` | True | False | - |
| `title` | `VARCHAR(180)` | False | False | - |
| `slug` | `VARCHAR(200)` | False | False | - |
| `subtitle` | `VARCHAR(255)` | False | False |  |
| `price_start_per_person` | `NUMERIC(12, 2)` | False | False | 0 |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `country_id` | `INTEGER` | True | False | - |
| `state_id` | `INTEGER` | True | False | - |
| `city_id` | `INTEGER` | True | False | - |
| `category_id` | `INTEGER` | True | False | - |
| `start_location` | `VARCHAR(150)` | False | False |  |
| `finish_location` | `VARCHAR(150)` | False | False |  |
| `number_of_days` | `INTEGER` | False | False | 1 |
| `number_of_hours` | `INTEGER` | True | False | - |
| `number_of_nights` | `INTEGER` | True | False | - |
| `max_group_size` | `INTEGER` | True | False | - |
| `min_booking_size` | `INTEGER` | True | False | - |
| `tour_language` | `VARCHAR(100)` | True | False | - |
| `suitable_age_range` | `VARCHAR(100)` | True | False | - |
| `tour_visibility` | `VARCHAR(20)` | False | False | public |
| `featured` | `BOOLEAN` | False | False | False |
| `short_description` | `TEXT` | False | False |  |
| `long_description` | `TEXT` | False | False |  |
| `pricing_type` | `VARCHAR(20)` | False | False | per_person |
| `offer_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `infant_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `single_supplement` | `NUMERIC(12, 2)` | False | False | 0 |
| `tax_percentage` | `FLOAT` | False | False | 0 |
| `service_fee` | `NUMERIC(12, 2)` | False | False | 0 |
| `gateway_fee_percentage` | `FLOAT` | False | False | 0 |
| `booking_deposit` | `NUMERIC(12, 2)` | False | False | 0 |
| `deposit_type` | `VARCHAR(20)` | False | False | fixed |
| `deposit_percentage` | `FLOAT` | True | False | - |
| `deposit_cutoff_days` | `INTEGER` | True | False | - |
| `balance_payment_deadline_days` | `INTEGER` | True | False | - |
| `requires_supplier_confirmation` | `BOOLEAN` | False | False | True |
| `seo_title` | `VARCHAR(180)` | False | False |  |
| `seo_description` | `VARCHAR(255)` | False | False |  |
| `seo_keywords` | `VARCHAR(255)` | False | False |  |
| `focus_keyword` | `VARCHAR(180)` | True | False | - |
| `canonical_url` | `VARCHAR(500)` | True | False | - |
| `open_graph_image` | `VARCHAR(255)` | True | False | - |
| `search_visibility` | `BOOLEAN` | False | False | True |
| `image_alt_text` | `VARCHAR(180)` | False | False |  |
| `banner_image` | `VARCHAR(255)` | False | False |  |
| `map_image` | `VARCHAR(255)` | False | False |  |
| `mobile_cover_image` | `VARCHAR(255)` | True | False | - |
| `tour_video_url` | `VARCHAR(500)` | True | False | - |
| `brochure_pdf` | `VARCHAR(255)` | True | False | - |
| `status` | `VARCHAR(20)` | False | False | draft |
| `commission_percentage` | `NUMERIC(5, 2)` | True | False | - |
| `admin_markup_percentage` | `NUMERIC(5, 2)` | True | False | - |
| `created_by` | `INTEGER` | True | False | - |
| `updated_by` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `state_id` references `states.id`
- Column `category_id` references `tour_categories.id`
- Column `city_id` references `cities.id`
- Column `country_id` references `countries.id`
- Column `updated_by` references `users.id`
- Column `created_by` references `users.id`
- Column `supplier_id` references `suppliers.id`

### `user_roles`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `user_id` | `INTEGER` | False | False | - |
| `role_id` | `INTEGER` | False | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `user_id` references `users.id`
- Column `role_id` references `roles.id`

### `user_sessions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `user_id` | `INTEGER` | False | False | - |
| `session_id` | `VARCHAR(120)` | False | False | - |
| `current_refresh_jti` | `VARCHAR(64)` | True | False | - |
| `ip_address` | `VARCHAR(100)` | True | False | - |
| `user_agent` | `VARCHAR(255)` | True | False | - |
| `status` | `VARCHAR(30)` | False | False | active |
| `revoked_at` | `DATETIME` | True | False | - |
| `last_seen_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `user_id` references `users.id`

### `user_status_history`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `user_id` | `INTEGER` | False | False | - |
| `from_status` | `VARCHAR(40)` | True | False | - |
| `to_status` | `VARCHAR(40)` | False | False | - |
| `reason` | `VARCHAR(500)` | True | False | - |
| `changed_by` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | False | False | - |

**Foreign Keys:**
- Column `changed_by` references `users.id`
- Column `user_id` references `users.id`

### `users`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `name` | `VARCHAR(150)` | False | False | - |
| `email` | `VARCHAR(150)` | False | False | - |
| `phone` | `VARCHAR(30)` | False | False |  |
| `profile_image` | `VARCHAR(255)` | False | False |  |
| `address` | `VARCHAR(255)` | False | False |  |
| `country` | `VARCHAR(100)` | False | False |  |
| `state` | `VARCHAR(100)` | False | False |  |
| `city` | `VARCHAR(100)` | False | False |  |
| `pincode` | `VARCHAR(20)` | False | False |  |
| `password` | `VARCHAR(255)` | True | False | - |
| `role_id` | `INTEGER` | True | False | - |
| `is_active` | `BOOLEAN` | True | False | True |
| `approval_status` | `VARCHAR(30)` | False | False | approved |
| `user_type` | `VARCHAR(20)` | True | False | - |
| `country_code` | `VARCHAR(8)` | False | False |  |
| `mobile_number` | `VARCHAR(20)` | True | False | - |
| `email_verified` | `BOOLEAN` | False | False | False |
| `password_created_at` | `DATETIME` | True | False | - |
| `account_status` | `VARCHAR(40)` | False | False | ACTIVE |
| `admin_verified` | `BOOLEAN` | False | False | False |
| `admin_verified_at` | `DATETIME` | True | False | - |
| `admin_verified_by` | `INTEGER` | True | False | - |
| `deactivated_at` | `DATETIME` | True | False | - |
| `deactivated_by` | `INTEGER` | True | False | - |
| `deactivation_reason` | `VARCHAR(500)` | True | False | - |
| `last_login_at` | `DATETIME` | True | False | - |
| `reset_password_token` | `VARCHAR(255)` | True | False | - |
| `reset_password_expires_at` | `DATETIME` | True | False | - |
| `email_verified_at` | `DATETIME` | True | False | - |
| `email_verification_token` | `VARCHAR(255)` | True | False | - |
| `email_verification_expires_at` | `DATETIME` | True | False | - |
| `otp_code_hash` | `VARCHAR(255)` | True | False | - |
| `otp_expires_at` | `DATETIME` | True | False | - |
| `otp_attempts` | `INTEGER` | True | False | 0 |
| `token_version` | `INTEGER` | False | False | 0 |
| `two_factor_enabled` | `BOOLEAN` | False | False | False |
| `two_factor_secret` | `VARCHAR(255)` | True | False | - |
| `two_factor_backup_codes` | `TEXT` | True | False | - |
| `force_password_reset` | `BOOLEAN` | False | False | False |
| `failed_login_attempts` | `INTEGER` | False | False | 0 |
| `locked_until` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `role_id` references `roles.id`
- Column `deactivated_by` references `users.id`
- Column `admin_verified_by` references `users.id`
