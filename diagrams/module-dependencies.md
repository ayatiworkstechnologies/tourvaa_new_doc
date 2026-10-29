# Architectural Module Dependencies & Communication Graph

This document details the inter-module dependency graph, showcasing the communication pathways and data flow among all 20 business modules in the Tourvaa platform.

---

## 1. Complete System Module Dependency Graph

```mermaid
graph LR
    subgraph IDENTITY["Identity & Governance"]
        AUTH[01. Auth & Users]
        ROLES[Roles & Permissions]
        AUDIT[19. Audit Logging]
        SETTINGS[20. Settings & Currency]
    end

    subgraph CATALOG["Catalog & Inventory"]
        GEO[13. Destination Guides & Geo]
        TOURS[02. Tours & Catalog]
        VERSIONS[03. Tour Versions & Approval]
        VIATOR[17. External Day Tours]
    end

    subgraph COMMERCIALS["Commercial Hub & Partners"]
        SUPPLIERS[08. Suppliers & Ledger]
        AGENTS[09. Agents & Resellers]
        AFFILIATES[10. Affiliate Program]
        CUSTOMERS[11. Customer Management]
    end

    subgraph TRANSACTION["Transaction Engine"]
        BOOKINGS[04. Booking Engine]
        CHECKOUT[05. Checkout & Payments]
        INVOICES[06. Invoices & Receipts]
        REFUNDS[07. Cancellations & Refunds]
    end

    subgraph ENGAGEMENT["Engagement & Support"]
        CMS[12. Website CMS & Blog]
        MESSAGING[14. Realtime Messaging]
        NOTIF[15. Notification Engine]
        CHATBOT[16. AI Chatbot & RAG]
        REPORTS[18. Reports & Analytics]
    end

    %% Dependencies
    AUTH --> ROLES
    AUTH --> AUDIT
    
    TOURS --> GEO
    TOURS --> SUPPLIERS
    VERSIONS --> TOURS
    VERSIONS --> AUTH
    VIATOR --> GEO
    
    BOOKINGS --> TOURS
    BOOKINGS --> CUSTOMERS
    BOOKINGS --> SUPPLIERS
    BOOKINGS --> AGENTS
    BOOKINGS --> AFFILIATES
    
    CHECKOUT --> BOOKINGS
    CHECKOUT --> SETTINGS
    INVOICES --> BOOKINGS
    INVOICES --> CHECKOUT
    REFUNDS --> BOOKINGS
    REFUNDS --> CHECKOUT
    
    SUPPLIERS --> BOOKINGS
    AGENTS --> BOOKINGS
    AFFILIATES --> BOOKINGS
    
    BOOKINGS --> NOTIF
    BOOKINGS --> MESSAGING
    MESSAGING --> AUTH
    
    CHATBOT --> TOURS
    CHATBOT --> CMS
    CMS --> GEO
    
    REPORTS --> BOOKINGS
    REPORTS --> CHECKOUT
    REPORTS --> SUPPLIERS
    REPORTS --> AGENTS
```

---

## 2. Structural Layering & Separation of Concerns

The architecture strictly adheres to a layered hierarchy:
1. **Foundation Tier**: Database engines, Redis cache, filesystem roots, encryption utilities (`app/utils/money.py`, `app/utils/distributed_lock.py`).
2. **Persistence Tier**: 138 SQLAlchemy declarative models in `app/models/` defining primary keys, indexes, foreign key constraints, and cascade policies.
3. **Domain Service Tier**: 56 business domain services in `app/services/` encapsulating business logic, calculation formulas, and external API requests.
4. **Interface / Transport Tier**: 51 FastAPI routers in `app/routers/` handling HTTP request deserialization, Pydantic validation, authorization dependencies, and JSON serialization.
5. **Client Presentation Tier**: Next.js 16 frontend consuming the API via same-origin proxied HTTP requests and direct WebSocket streams.
