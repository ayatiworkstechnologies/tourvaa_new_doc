# 12 — External Third-Party Integrations

This document catalogs all external third-party service integrations, API credentials, webhook verification, and fault-tolerance mechanisms.

---

## 1. Third-Party Integrations Summary

| Integration | Business Purpose | Architecture Implementation | Status |
|---|---|---|---|
| **Stripe** | Credit/debit card checkout, manual pre-authorization holds, captures, refunds. | [`app/services/payments_gateway.py`](../tourvaa-admin-backend/app/services/payments_gateway.py) (StripeGateway) | **Active & Verified** |
| **PayPal** | PayPal wallet checkout, order authorizations, captures, voids. | [`app/services/payments_gateway.py`](../tourvaa-admin-backend/app/services/payments_gateway.py) (PayPalGateway) | **Active & Verified** |
| **Viator** | Day tours, activities, and experiences catalog supplementation. | [`app/integrations/viator/`](../tourvaa-admin-backend/app/integrations/viator) & [`app/services/viator.py`](../tourvaa-admin-backend/app/services/viator.py) | **Active & Verified** |
| **Cloudinary** | Image CDN, compression, thumbnail generation for public tours & CMS. | Cloudinary Python SDK via [`app/routers/uploads.py`](../tourvaa-admin-backend/app/routers/uploads.py) | **Active & Verified** |
| **SMTP Mailer** | Transactional and lifecycle email delivery. | Python `smtplib` via [`app/utils/mailer.py`](../tourvaa-admin-backend/app/utils/mailer.py) | **Active & Verified** |
| **WebPush (VAPID)**| In-browser push notifications for booking alerts. | `pywebpush` via [`app/services/notifications_push.py`](../tourvaa-admin-backend/app/services/notifications_push.py) | **Active & Verified** |
| **FastEmbed / ONNX**| Self-hosted vector embeddings for AI chatbot RAG search. | `fastembed` & `onnxruntime` (`BAAI/bge-small-en-v1.5`) | **Active & Verified** |
| **GeoIP (ip-api)** | Best-effort IP geolocation for browsing currency and locale. | HTTP lookup via [`app/services/currency.py`](../tourvaa-admin-backend/app/services/currency.py) | **Active & Verified** |
| **Google OAuth** | Social login for customer registration and authentication. | [`app/routers/google_auth.py`](../tourvaa-admin-backend/app/routers/google_auth.py) | **Active & Verified** |
| **Elfsight Translator**| Multi-lingual site translation widget on public storefront. | Script embed configured with CSP headers in `next.config.ts` | **Active & Verified** |
