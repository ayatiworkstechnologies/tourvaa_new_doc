# 02 — Technology Stack & Verified Versions

This document details the complete, verified technology stack across the frontend, backend, database, testing, and deployment infrastructure.

---

## 1. Backend Technology Stack (`tourvaa-admin-backend`)

| Category | Technology | Verified Version | Purpose & Architecture Role |
|---|---|---|---|
| **Language Runtime** | Python | `3.12` | Core programming language runtime. |
| **Web Framework** | FastAPI | `0.139.2` | High-performance asynchronous REST API framework based on Starlette and Pydantic. |
| **ASGI Server** | Uvicorn | `0.51.0` | Asynchronous Server Gateway Interface server. |
| **WebSockets** | websockets | `15.0.1` | Native WebSocket handshake support for Uvicorn (`/api/ws/messages`). |
| **ORM Framework** | SQLAlchemy | `2.0.51` | Object-Relational Mapping with 2.0 declarative typing and connection pooling. |
| **Database Driver** | PyMySQL | `1.2.0` | Pure-Python MySQL client driver. |
| **Database Migrations** | Alembic | `1.18.5` | Schema revision tracking and automated migration execution. |
| **Configuration** | Pydantic Settings | `2.14.2` | Strongly typed environment variable loading and validation. |
| **Authentication & JWT**| Python-Jose | `3.5.0` | Cryptographic JWT signing and decoding (HS256). |
| **Password Hashing** | Passlib & Bcrypt | `passlib 1.7.4`, `bcrypt 4.0.1` | Salted Bcrypt password hashing. |
| **Form & Multi-part** | Python-Multipart | `0.0.32` | File upload and multipart form data streaming. |
| **Email Validation** | Email-Validator | `2.3.0` | Robust RFC-compliant email address validation. |
| **HTTP Clients** | Requests & HTTPX | `requests 2.34.2`, `httpx 0.28.1` | Synchronous and asynchronous external API clients (Stripe, PayPal, Viator). |
| **AI Embeddings (RAG)** | FastEmbed & ONNX | `fastembed 0.8.0`, `onnxruntime 1.28.0` | CPU-optimized local vector embeddings (`BAAI/bge-small-en-v1.5`). |
| **Push Notifications** | PyWebPush | `2.3.0` | Standard WebPush VAPID notification delivery. |
| **PDF Generation** | ReportLab & Pillow | `reportlab 5.0.0`, `Pillow 12.3.0` | Programmatic PDF generation for invoices, receipts, and itineraries. |
| **Caching & Pub/Sub** | Redis | `8.0.1` | Distributed locks, rate limiting, and cross-worker WebSocket pub/sub. |
| **Media Storage** | Cloudinary | `1.45.0` | Media upload and image transformations for public tours and CMS assets. |
| **HTML Sanitization** | Bleach | `6.4.0` | HTML sanitization for blog content and CMS rich-text descriptions. |
| **Data Encryption** | Cryptography | `49.0.0` | AES-256 encryption for database-persisted API keys and payment secrets. |
| **Spreadsheet Engine** | OpenPyXL | `3.1.5` | Excel generation and bulk tour import/export processing. |
| **Two-Factor Auth** | PyOTP & QRCode | `pyotp 2.10.0`, `qrcode 8.2` | Time-based One-Time Password (TOTP) generation and QR code rendering. |
| **Phone Number Parsing**| PhoneNumbers | `9.0.41` | International E.164 phone number formatting and validation. |

---

## 2. Frontend Technology Stack (`tourvaa-admin-frontend`)

| Category | Technology | Verified Version | Purpose & Architecture Role |
|---|---|---|---|
| **Language Runtime** | Node.js | `22.x LTS` | JavaScript runtime environment. |
| **Framework** | Next.js | `16.3.1` | React App Router framework supporting hybrid SSR and client-side rendering. |
| **UI Library** | React & React DOM | `19.2.4` | Modern React component architecture. |
| **Type System** | TypeScript | `5.x` | Static type checking and interface contracts. |
| **Styling Engine** | Tailwind CSS | `4.x` (`@tailwindcss/postcss`) | Next-generation utility-first CSS styling engine. |
| **HTTP Client** | Axios | `1.17.0` | Client-side HTTP requests with credentials and global interceptors. |
| **Form Management** | React Hook Form | `7.78.0` | Performant form state management and input validation. |
| **Iconography** | React Icons & Flag Icons| `react-icons 5.7.0`, `flag-icons 7.5.0` | Feather, Lucide, FontAwesome icons and country flag SVG assets. |
| **Data Visualization** | Recharts | `3.9.0` | Declarative SVG charting for admin and supplier financial dashboards. |
| **Typography Fonts** | Fontsource | `@fontsource-variable/onest`, `@fontsource/inter` | Self-hosted web typography fonts. |
| **Phone Input Helper** | LibPhoneNumber-JS| `1.13.12` | Client-side international phone input masking. |

---

## 3. Testing & Infrastructure Stack

| Category | Technology | Verified Version | Purpose & Architecture Role |
|---|---|---|---|
| **Backend Testing** | Pytest | `9.1.1` | Unit, integration, and security testing framework (111 test files). |
| **Frontend Unit Tests**| Vitest | `4.1.11` | Vite-native unit test runner for React components and utilities. |
| **Component Testing** | Testing Library | `@testing-library/react 16.3.2` | DOM testing utilities and user-event simulation. |
| **End-to-End Testing** | Playwright | `1.61.1` | Cross-browser automated browser testing (Chromium/Firefox/WebKit). |
| **Containerization** | Docker | Engine 24+ (syntax 1.7) | Multi-stage Docker builds for backend (Python) and frontend (Node.js). |
| **Continuous Integration**| GitHub Actions | Workflows `ci-cd.yml` | Automated linting, test suites, vulnerability scans (Trivy), and container publishing. |
