# Module 13: Destination Guides & Geo Reference

## 1. Module Overview

| Attribute | Details |
|---|---|
| **Module Name** | Destination Guides & Geo Reference |
| **Business Purpose** | Manages geographical data (countries, states, cities), destination landing pages, curated travel guides, season weather advice ('When to Go'), and currency mapping. |
| **Supported Roles** | Public Visitors, Admins |
| **Permissions Required** | `countries.view, countries.edit, cities.view, cities.edit` |

---

## 2. Functional & Business Workflows

### 2.1 Workflow Architecture
```mermaid
flowchart TD
    GEO_DB[Geo Database: Country/State/City] --> DEST_PAGE[Destination Guide: /destinations/{slug}]
    DEST_PAGE --> HERO[Hero Section & Country Map]
    DEST_PAGE --> WHY[Why Visit & Best Time to Go]
    DEST_PAGE --> TOURS_LIST[Curated Multi-Day Tours in Country]
    DEST_PAGE --> EXT_TOURS[Viator External Day Trips]
```

### 2.2 Functional Capabilities
- **Core Operations**: Fully implemented CRUD lifecycle operations backing the portal interfaces.
- **Validation Rules**: Strict Pydantic and React Hook Form validation rules enforcing data integrity and sanitization.
- **Error Handling**: Standardized error responses returning structured JSON codes and human-readable messages.

---

## 3. Technical Implementation Details

### 3.1 Source Files & Entry Points
- **Frontend Pages**:
- [`/destinations`](../../tourvaa-admin-frontend/src/app/%28public%29/destinations/page.tsx)
- [`/destinations/[slug]`](../../tourvaa-admin-frontend/src/app/%28public%29/destinations/[slug]/page.tsx)
- [`/travel-advice`](../../tourvaa-admin-frontend/src/app/%28public%29/travel-advice/page.tsx)
- [`/admin/settings/countries`](../../tourvaa-admin-frontend/src/app/admin/settings/countries/page.tsx)
- [`/admin/settings/cities`](../../tourvaa-admin-frontend/src/app/admin/settings/cities/page.tsx)
- **Backend Routers**:
- [`app/routers/cms_geo.py`](../../tourvaa-admin-backend/app/routers/cms_geo.py)
- [`app/routers/cms_geo_seed.py`](../../tourvaa-admin-backend/app/routers/cms_geo_seed.py)
- [`app/routers/public.py`](../../tourvaa-admin-backend/app/routers/public.py)
- **Domain Services**:
- [`app/services/cms.py`](../../tourvaa-admin-backend/app/services/cms.py)
- [`app/services/currency.py`](../../tourvaa-admin-backend/app/services/currency.py)

### 3.2 Database Entities
- **Primary Database Tables**:
- `countries`
- `states`
- `cities`
- `cms_country_pages`
- `cms_favourite_countries`
