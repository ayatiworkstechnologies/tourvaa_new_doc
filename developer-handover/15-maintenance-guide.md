# Chapter 15: Platform Maintenance & Operational Runbook

## 1. Routine Maintenance Schedule

| Cadence | Task Description | Target Component | Procedure |
|---|---|---|---|
| **Daily** | Automated Database Backup | MySQL Server | Execute `mysqldump` snapshot and upload to offsite S3 bucket. |
| **Daily** | Stale Booking Hold Cleanup | Bookings Table | Run automatically via startup timer or trigger `POST /api/bookings/expire-stale`. |
| **Weekly**| Disk Storage & Log Rotation | Application Hosts | Check `/data/storage` volume usage; rotate Nginx/Uvicorn log files. |
| **Monthly**| Dependency Vulnerability Scan | Node / Python | Run `npm audit` and `pip-audit` to detect CVEs in third-party packages. |
| **Quarterly**| SSL Certificate & Key Rotation | Edge / Config | Verify Let's Encrypt auto-renewal; rotate JWT and payment webhook secrets. |
