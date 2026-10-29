# Chapter 10 — Backup, Rollback & Disaster Recovery

## 1. Rollback Trigger Conditions

A rollback must be initiated immediately if any of the following occur within the first 60 minutes of release:
1. **Critical Health Failure**: Backend `/api/health` or Frontend `/` returns persistent HTTP 5xx errors.
2. **Authentication Lockout**: Users, agents, or administrators cannot authenticate across multiple portals.
3. **Payment Failure**: Webhooks fail to record or checkout captures fail consistently.
4. **Data Corruption Alert**: Database logs indicate constraint violations or foreign key corruption.

---

## 2. Granular Rollback Procedures

### Procedure A: Application Container Rollback (No Schema Change)
If the database schema was not modified, rolling back is purely an image swap:

```bash
# 1. Rollback Frontend Container to previous stable tag
docker stop tourvaa-frontend
docker run -d --name tourvaa-frontend-rollback ... ghcr.io/ayatiworks/tourvaa-admin-frontend:v0.9.8

# 2. Rollback Backend Container to previous stable tag
docker stop tourvaa-backend
docker run -d --name tourvaa-backend-rollback ... ghcr.io/ayatiworks/tourvaa-admin-backend:v0.9.8

# 3. Verify health
curl -f http://127.0.0.1:8000/api/health
curl -f http://127.0.0.1:3000/
```

### Procedure B: Full Disaster Recovery (Database & Application Restore)
If database state was compromised:

```bash
# 1. Place application into maintenance mode at reverse proxy
cp /etc/nginx/conf.d/maintenance.conf /etc/nginx/conf.d/default.conf
nginx -s reload

# 2. Restore database from pre-deployment snapshot using protected credentials
mysql --defaults-extra-file=/etc/mysql/secure_client.cnf tourvaa < /backup/tourvaa_pre_deploy.sql

# 3. Restart previous container versions
docker restart tourvaa-backend-previous tourvaa-frontend-previous

# 4. Remove maintenance mode
cp /etc/nginx/conf.d/production.conf /etc/nginx/conf.d/default.conf
nginx -s reload
```

---

## 3. Data Safety & Preservation Guarantees

- **Snapshot Storage**: Uploaded documents in `/data/storage` and `/data/private-docs` are kept on persistent host volumes independent of container lifecycles.
- **Financial Audit Trails**: All financial snapshots in `invoices` and `bookings` remain immutable. No rollback procedure will truncate or overwrite live financial records.
