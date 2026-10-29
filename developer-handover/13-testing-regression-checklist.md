# Chapter 13: QA Architecture & Regression Testing Checklist

## 1. Automated Test Execution Commands

### 1.1 Backend Pytest Execution (110 Test Suites)
```bash
# Navigate to backend
cd tourvaa-admin-backend

# Run complete test suite
pytest

# Run core authentication tests only
pytest tests/test_02_auth.py tests/test_03_rbac.py

# Run bookings & financial tests
pytest tests/test_20_bookings.py tests/test_22_payments.py
```

### 1.2 Frontend Unit & Integration Tests (Vitest)
```bash
# Navigate to frontend
cd tourvaa-admin-frontend

# Run Vitest unit tests
npm run test

# Run specific component test
npx vitest run tests/unit/CustomerBookings.test.tsx
```

### 1.3 Playwright E2E Browser Tests
```bash
# Run headless E2E audit
npx playwright test

# Run UI mode with visual inspector
npx playwright test --ui
```

---

## 2. Critical Regression Checklist for Deployments

Before releasing any code change to staging or production, verify:
- [ ] Authentication: Public login, 2FA prompt, password reset, and logout invalidation pass.
- [ ] Catalog: Tour search, date selection, and pricing tier calculation return valid figures.
- [ ] Checkout: Cart addition, discount coupon application, and payment gateway intent creation succeed.
- [ ] Bookings: Booking record is created in `pending_payment` and transitions to `confirmed` upon payment webhook.
- [ ] Supplier: Supplier portal receives booking notification and can accept/decline.
- [ ] Agent: Agent balance deduction and credit limits calculate accurately.
- [ ] Migrations: `alembic upgrade head` executes cleanly on fresh test database.
