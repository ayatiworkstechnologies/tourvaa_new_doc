# 20 — Troubleshooting & Incident Response Runbook

## 1. Common Operational Issues & Playbooks

### Issue 1: Database Migration Mismatch on Startup
- **Symptom**: Backend crashes on startup with: `RuntimeError: Database migration mismatch: database head(s) [...], application head(s) [...]`.
- **Root Cause**: The running database schema is behind the deployed code commit.
- **Playbook**:
  ```powershell
  cd tourvaa-admin-backend
  alembic upgrade head
  ```

### Issue 2: Refusing to Start with Unsafe Production Configuration
- **Symptom**: Backend crashes with: `RuntimeError: Refusing to start with unsafe production configuration`.
- **Root Cause**: `APP_DEBUG=true`, default passwords, or missing webhook secrets in production.
- **Playbook**: Inspect `.env` against section 1.1 of [`inventories/environment-variables.md`](inventories/environment-variables.md) and supply required strong secrets.

### Issue 3: Stale Booking Holding Calendar Seats
- **Symptom**: Customer complains a departure date appears sold out, but no completed booking exists.
- **Root Cause**: An abandoned draft booking is holding seats before the 60-minute expiry sweep has fired.
- **Playbook**: Admin can navigate to `/admin/bookings`, locate the `pending_payment` booking, and click "Cancel Booking", immediately releasing seats back to `TourCalendar`.

### Issue 4: WebSocket Connection Fails (/api/ws/messages)
- **Symptom**: Chat messages do not update in real time; browser logs WebSocket connection failure.
- **Root Cause**: `NEXT_PUBLIC_WS_URL` is pointing to an unreachable host or `websockets` dependency is missing.
- **Playbook**: Verify `NEXT_PUBLIC_WS_URL` matches the backend host and uses `ws://` (local) or `wss://` (production).
