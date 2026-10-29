# 13 — Environment Configuration & Secrets Management

This document serves as the guide for configuring Tourvaa across development, staging, and production environments.

---

## 1. Secrets Security & AES Database Encryption

Sensitive credentials (such as Stripe Secret Keys, PayPal Client Secrets, SMTP Passwords, and Viator API Keys) are **never stored as plaintext** in the database.
- The platform uses **AES-256-GCM encryption** implemented in `app/utils/crypto.py`.
- The encryption key is sourced from `SETTINGS_ENCRYPTION_KEY` (a 64-character hexadecimal string representing a 256-bit key).
- **Critical Rule**: Once generated, `SETTINGS_ENCRYPTION_KEY` must never be altered in a production environment; changing it will corrupt all previously encrypted database secrets.

---

## 2. Production Startup Validation

The backend enforces fail-safe configuration validation at startup in [`app/main.py`](../tourvaa-admin-backend/app/main.py):
1. Rejects startup if `APP_DEBUG=true` in production.
2. Rejects startup if `SUPER_ADMIN_PASSWORD` is left as default `"Admin@123"`.
3. Rejects startup if `ADMIN_JWT_SECRET_KEY` or `NORMAL_JWT_SECRET_KEY` are shorter than 32 characters or identical.
4. Rejects startup if `ALLOWED_ORIGINS="*"` in production (credentials disabled by browsers on wildcard CORS).
5. Rejects startup if `STRIPE_WEBHOOK_SECRET` or `PAYPAL_WEBHOOK_ID` are missing.

The complete environment variable inventory is cataloged in [`inventories/environment-variables.md`](inventories/environment-variables.md).
