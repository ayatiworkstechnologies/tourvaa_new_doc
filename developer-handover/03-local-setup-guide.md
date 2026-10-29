# Chapter 03: Comprehensive Local Development Setup Guide

## 1. Backend Setup Step-by-Step

### Step 1.1: Create & Activate Python Virtual Environment
Navigate to the backend directory and create a dedicated Python 3.12 virtual environment:
```powershell
# Windows PowerShell
cd tourvaa-admin-backend
python -m venv venv
.\venv\Scripts\Activate.ps1
```

```bash
# macOS / Linux
cd tourvaa-admin-backend
python3.12 -m venv venv
source venv/bin/activate
```

### Step 1.2: Install Python Dependencies
```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### Step 1.3: Configure Environment Variables
Copy the template configuration to create `.env`:
```powershell
# Windows
Copy-Item .env.example .env

# Linux / macOS
cp .env.example .env
```

Edit `.env` and verify your local database connection:
```ini
DATABASE_URL=mysql+pymysql://root:password@localhost:3306/tourvaa_db
ENVIRONMENT=development
SECRET_KEY=dev-secret-key-do-not-use-in-production-12345
JWT_SECRET=dev-jwt-secret-do-not-use-in-production-12345
CORS_ORIGINS=["http://localhost:3000","http://127.0.0.1:3000"]
```

### Step 1.4: Initialize Database & Run Migrations
Ensure MySQL is running and the database exists:
```sql
CREATE DATABASE IF NOT EXISTS tourvaa_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

Execute Alembic migrations to construct all 138 database tables:
```bash
python -m alembic upgrade head
```

Seed initial administrative roles and default settings:
```bash
python -m app.seed
```

### Step 1.5: Start the Backend Development Server
```bash
uvicorn app.main:app --host 127.0.0.1 --port 8000 --reload
```
- **Verification**: Open browser at `http://localhost:8000/docs` to view the interactive OpenAPI documentation.

---

## 2. Frontend Setup Step-by-Step

### Step 2.1: Install Node Dependencies
Open a second terminal, navigate to the frontend directory:
```bash
cd tourvaa-admin-frontend
npm install
```

### Step 2.2: Configure Frontend Environment Variables
Copy `.env.example` to `.env.local`:
```bash
cp .env.example .env.local
```
Verify the API base URL:
```ini
NEXT_PUBLIC_API_URL=http://localhost:8000/api
```

### Step 2.3: Start Frontend Dev Server
```bash
npm run dev
```
- **Verification**: Open `http://localhost:3000` in your browser. The Tourvaa storefront will load.

---

## 3. Health Check & Initial Login Verification

1. **Backend Health Check**:
   ```bash
   curl http://localhost:8000/api/health
   # Expected response: {"status":"healthy","database":"connected"}
   ```
2. **Admin Portal Login**:
   - URL: `http://localhost:3000/admin/login`
   - Default seeded credentials are provided in `tourvaa-admin-backend/app/seed.py`.
