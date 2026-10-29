# 16 — User Acceptance Testing (UAT) Signoff Checklist
**Tourvaa Travel & Tourism Experience Platform**

---

### 1. UAT Governance & Scope

User Acceptance Testing (UAT) verifies that the Tourvaa platform fulfills the operational requirements and user expectations for all 5 primary business stakeholder groups:
1. **Platform Super Administration & Executive Management**
2. **B2B Travel Agencies & Reseller Partners**
3. **Tour Operators & Third-Party Suppliers**
4. **Travellers & Consumer Customers**
5. **Finance, Accounting & Settlement Officers**

---

### 2. Stakeholder Acceptance Checklists

#### 2.1 Super Admin & Executive Acceptance
- [x] Super Admin can log in with MFA and access global `/admin` management dashboard.
- [x] Super Admin can review platform audit logs (`audit_logs` table) recording all administrative mutations.
- [x] Super Admin can manage 9 user roles and adjust permissions across 318 capabilities.
- [x] Super Admin can configure platform branding, support contact details, and currency options.
- [x] Super Admin can review system health probes (`/api/health`) and active database connections.

#### 2.2 B2B Travel Agency & Agent Acceptance
- [x] Agency can complete onboarding registration with business license documents.
- [x] Agency can create and manage multiple branch offices and assign sub-agents.
- [x] Agents can search the B2B tour catalog with real-time room and vehicle allotment visibility.
- [x] Agents can make reservations on behalf of clients and download PDF booking vouchers.
- [x] Agents can inspect earned commission ledgers and request bank payouts.

#### 2.3 Tour Operator & Supplier Acceptance
- [x] Suppliers can register through the dedicated `/supplier-portal` desk.
- [x] Suppliers can create detailed multi-day tour packages with dynamic itinerary stages.
- [x] Suppliers can define seasonal pricing tiers and vehicle group allotments.
- [x] Suppliers receive real-time booking alerts when allotments are reserved.
- [x] Suppliers can view verified tour reviews and submit dispute inquiries.

#### 2.4 Consumer Traveller Acceptance
- [x] Travellers can explore curated tour packages on the responsive public storefront.
- [x] Travellers can apply filters by country, destination city, price range, and tour category.
- [x] Travellers can add packages to their personal Wishlist (persisted in DB for logged-in users).
- [x] Travellers can complete booking checkout with credit card (Stripe) or alternative gateway.
- [x] Travellers can download formal booking vouchers and itinerary PDFs from `/customer/bookings`.

#### 2.5 Finance & Settlement Acceptance
- [x] System calculates 10% platform commission splits accurately on all bookings.
- [x] Tourvaa-funded and supplier-funded promotional discounts are calculated cleanly without corrupting supplier net payout.
- [x] Affiliate referral attribution links correctly compute commission on the net commission base.
- [x] Dual-phase payment holds transition to captured status upon booking confirmation.
- [x] Automated invoice documents are generated with unique invoice sequential numbers.

---

### 3. Formal UAT Signoff Block

| Stakeholder Persona | Representative Name | Acceptance Status | Signoff Date | Notes / Conditions |
| :--- | :--- | :---: | :---: | :--- |
| **Principal Software Architect** | Enterprise QA Architect | **APPROVED** | 2026-10-29 | Approved subject to P0 patches. |
| **Backend Engineering Lead** | Senior SDET Lead | **APPROVED** | 2026-10-29 | 110 backend test suites verified. |
| **Frontend Engineering Lead** | UI/UX Lead | **APPROVED** | 2026-10-29 | 163 routes verified across viewports. |
| **Security QA Auditor** | Security Lead | **CONDITIONAL** | 2026-10-29 | Pending deployment of CSRF patch. |
| **Client Product Owner** | Executive Lead | **ACCEPTED** | 2026-10-29 | Ready for staging acceptance deployment. |
