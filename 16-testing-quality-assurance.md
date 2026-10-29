# 16 — Testing & Quality Assurance Architecture

## 1. Test Strategy Overview

Tourvaa employs a comprehensive, multi-tiered testing strategy:
- **Backend Testing**: 111 Pytest test files covering unit models, business services, payment workflows, RBAC permission matrices, and migrations.
- **Frontend Unit Testing**: 18 Vitest test suites verifying UI component rendering, form validation rules, currency math, and custom hooks.
- **Contract Testing**: 15 Node.js test runners validating API route signatures and cross-repository contracts.
- **End-to-End Testing**: 8 Playwright test specifications executing complete browser workflows against live DOM elements.

---

## 2. Executing Tests Locally

### Backend Test Suite
```powershell
cd tourvaa-admin-backend
pytest tests -v
```

### Frontend Unit Tests (Vitest)
```powershell
cd tourvaa-admin-frontend
npm run test:unit
```

### Frontend TypeScript Verification
```powershell
cd tourvaa-admin-frontend
npx tsc --noEmit
```

### End-to-End Browser Tests (Playwright)
```powershell
cd tourvaa-admin-frontend
npx playwright test
```
