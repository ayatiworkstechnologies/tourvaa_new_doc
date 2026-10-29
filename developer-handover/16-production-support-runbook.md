# Chapter 16: Production Support & Incident Escalation Runbook

## 1. Incident Severity Definitions

- **SEV-1 (Critical Outage)**: Core booking or payment gateway unavailable; database offline; zero transactions processing. Immediate page to on-call architect. Response SLA: < 15 minutes.
- **SEV-2 (Major Degradation)**: A portal (e.g. Supplier or Agent) is inaccessible, but public bookings continue to operate. Response SLA: < 1 hour.
- **SEV-3 (Minor Defect)**: Cosmetic UI issue, non-critical report export timeout, or localized email delivery delay. Response SLA: < 24 hours.

---

## 2. On-Call Diagnostic Commands

```bash
# Check running container health
docker ps --format "table {{.Names}}	{{.Status}}	{{.Ports}}"

# Inspect real-time backend API logs
docker logs -f --tail 200 tourvaa-backend

# Check MySQL database connections
mysql -u root -p -e "SHOW STATUS LIKE 'Threads_connected';"

# Check Redis memory usage
redis-cli info memory
```
