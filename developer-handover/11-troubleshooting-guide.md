# Chapter 11: Production Troubleshooting & Incident Handling Playbooks

## 1. Top 16 Operational Incident Playbooks

| Incident Scenario | Symptoms | Likely Root Cause | Diagnostic & Resolution Procedure |
|---|---|---|---|
| **1. Backend Fails to Start** | Container logs show `Connection refused` or crash immediately. | MySQL service down or invalid `DATABASE_URL` credentials. | Check MySQL status (`mysqladmin ping`). Verify `.env` database user/password. |
| **2. Alembic Migration Locked** | Migration hangs or outputs `Lock wait timeout exceeded`. | Previous migration aborted leaving metadata table lock. | Check MySQL active locks: `SHOW PROCESSLIST;`. Kill blocking DDL query. |
| **3. CSRF 403 Forbidden** | Mutating API requests fail with `CSRF token missing or invalid`. | Missing `X-CSRF-Token` header in frontend Axios request. | Verify `tourvaa_csrf` cookie is present. Check request interceptor in `src/lib/api/client.ts`. |
| **4. 401 Unauthorized Loop** | User logged in but immediately redirected back to `/login`. | Expired refresh token or missing `tourvaa_refresh` cookie. | Check cookie domain settings. Clear browser cookies and re-authenticate. |
| **5. API 404 Not Found** | Calling an endpoint returns `404 Not Found`. | Router not mounted in `app/main.py` or URL prefix mismatch. | Verify router inclusion in `app/main.py:app.include_router(..., prefix='/api')`. |
| **6. API 500 Internal Error** | Endpoint crashes with unhandled exception. | Database constraint violation or missing null check. | Inspect backend stdout/stderr logs. Check database transaction state. |
| **7. CORS Policy Block** | Browser console: `No 'Access-Control-Allow-Origin' header`. | Request origin not listed in backend `CORS_ORIGINS`. | Update `CORS_ORIGINS` in `.env` to match client domain (e.g. `http://localhost:3000`). |
| **8. Image Upload Fails** | Upload returns `400 Bad Request` or `413 Payload Too Large`. | File size exceeds limit or disallowed MIME extension. | Verify file format is in `ALLOWED_IMAGE_EXTENSIONS`. Check Nginx `client_max_body_size`. |
| **9. Tour Images Broken (404)**| Image URLs return 404 Not Found on public website. | Storage directory not mounted or file write failed. | Verify `/data/storage` volume is persistent. Check file permissions `chown tourvaa:tourvaa`. |
| **10. Celery Tasks Stalled** | Background tasks (PDF vouchers, emails) not processing. | Redis broker unreachable or Celery worker process died. | Check Redis (`redis-cli ping`). Restart Celery worker: `celery -A app.core.celery worker`. |
| **11. High Memory on Exports**| Backend worker restarted due to OOM during CSV export. | `export_bookings` loaded >50k rows into RAM `io.StringIO`. | Implement pagination query filter (date range) or chunked cursor streaming. |
| **12. Stale Holds Not Expiring**| Tours show sold out even though bookings are unpaid. | Cron job timer failed or background sweep not executing. | Trigger manual sweep: `POST /api/bookings/expire-stale`. Verify timer in `app.main`. |
| **13. WebSocket Chat Fails** | Real-time chat messages not received without refresh. | WebSocket handshake rejected or reverse proxy missing upgrade. | Ensure Nginx config has `proxy_set_header Upgrade $http_upgrade;`. |
| **14. 502 Bad Gateway** | Nginx returns 502 Bad Gateway to browser. | Uvicorn process crashed or port 8000 not listening. | Inspect Uvicorn process health. Restart backend service. |
| **15. Frontend Hydration Error**| React hydration warning on button or dropdown click. | SSR HTML mismatched with client state. | Ensure dynamic date/time components use client-side formatting wrappers. |
| **16. Viator Sync Quota Error**| External day trips sync returns `429 Too Many Requests`. | Exceeded Viator Partner sandbox rate limit. | Throttle sync frequency in `app/routers/external_tours.py`. |
