# 14 — Local Development Setup Guide

Follow this guide to set up and run the Tourvaa platform locally.

---

## 1. Prerequisites

- **Python**: 3.12+ (64-bit)
- **Node.js**: 22.x LTS with npm
- **Database**: MySQL 8.0+ running on `localhost:3306`
- **Git**: Installed and configured

---

## 2. Backend Setup (`tourvaa-admin-backend`)

### Step 1: Navigate and Create Virtual Environment
```powershell
cd tourvaa-admin-backend
python -m venv venv
.\venv\Scripts\Activate.ps1
```

### Step 2: Install Dependencies
```powershell
python -m pip install --upgrade pip
pip install -r requirements.txt
pip install -r requirements-dev.txt
```

### Step 3: Configure `.env`
Create `.env` in `tourvaa-admin-backend/`:
```env
APP_ENV=development
APP_DEBUG=true
DATABASE_URL=mysql+pymysql://root:password@localhost:3306/tourvaa_db
JWT_SECRET_KEY=dev-secret-key-at-least-32-characters-long
ADMIN_JWT_SECRET_KEY=dev-admin-secret-at-least-32-characters
NORMAL_JWT_SECRET_KEY=dev-normal-secret-at-least-32-characters
FRONTEND_URL=http://localhost:3000
ALLOWED_ORIGINS=http://localhost:3000,http://127.0.0.1:3000
SETTINGS_ENCRYPTION_KEY=0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef
```

### Step 4: Run Migrations and Seed
```powershell
alembic upgrade head
python seed.py
```

### Step 5: Start FastAPI Server
```powershell
python -m uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```
- API Base: `http://localhost:8000`
- Swagger Docs: `http://localhost:8000/docs`
- Healthcheck: `http://localhost:8000/api/health`

---

## 3. Frontend Setup (`tourvaa-admin-frontend`)

### Step 1: Navigate and Install Dependencies
```powershell
cd tourvaa-admin-frontend
npm install
```

### Step 2: Configure `.env`
Create `.env` in `tourvaa-admin-frontend/`:
```env
API_PROXY_TARGET=http://127.0.0.1:8000
NEXT_PUBLIC_WS_URL=ws://127.0.0.1:8000
NEXT_PUBLIC_SITE_URL=http://localhost:3000
```

### Step 3: Start Next.js Development Server
```powershell
npm run dev
```
Open `http://localhost:3000` in your browser.
