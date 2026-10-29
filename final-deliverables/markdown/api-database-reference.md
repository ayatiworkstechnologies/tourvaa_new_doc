# TOURVAA PLATFORM: API & DATABASE TECHNICAL REFERENCE (CANONICAL EDITION)



---

# 07 — API Design, Standards & Endpoint Catalog

## 1. RESTful Design Conventions

Tourvaa's API adheres to strict REST conventions:
- **Base Prefix**: All application endpoints are mounted under `/api` (e.g. `/api/bookings`, `/api/tours`).
- **Affiliate Short Redirects**: Served directly under `/r/{code}` to facilitate clean, shareable referral URLs.
- **Resource Naming**: Plural nouns represent collections (`/api/tours`, `/api/suppliers`).
- **HTTP Verbs**:
  - `GET`: Safe, idempotent data retrieval.
  - `POST`: Resource creation or state-changing commands.
  - `PUT`: Complete resource replacement.
  - `PATCH`: Partial resource updates.
  - `DELETE`: Resource removal or soft-deletion.

---

## 2. API Metrics & Scale

Based on live OpenAPI inspection of the production codebase:
- **Total Registered Paths**: **594 distinct API paths**
- **Total API Operations**: **785 operations** across all HTTP methods
- **Functional Module Tags**: **61 unique operational categories**

The complete endpoint-by-endpoint inventory is cataloged in [`inventories/api-inventory.md`](../../inventories/api-inventory.md).

---

## 3. Standard Response Format & Error Codes

### Successful Response Format
```json
{
  "success": true,
  "data": { ... },
  "message": "Operation completed successfully"
}
```

### Standard Error Response Format
```json
{
  "success": false,
  "code": "SUPPLIER_APPROVAL_REQUIRED",
  "message": "Your supplier account must be approved before using this feature.",
  "detail": null
}
```

### Common HTTP Status Codes
- `200 OK`: Successful retrieval or synchronous update.
- `201 Created`: Successful creation of an entity.
- `400 Bad Request`: Validation failure or business constraint violation.
- `401 Unauthorized`: Missing, expired, or cryptographically invalid session token.
- `403 Forbidden`: Insufficient RBAC permissions or account pending approval.
- `404 Not Found`: Requested resource does not exist.
- `409 Conflict`: Unique constraint violation (e.g. duplicate email or slug).
- `422 Unprocessable Entity`: Schema validation failure by Pydantic.
- `500 Internal Server Error`: Unhandled server exception.

---

# Backend API Endpoint Inventory

**Total Verified Operations:** 785
**Total Functional Modules / Tags:** 62
**Base Path Prefix:** `/api`

| Method | Endpoint | Module Tag | Summary | Request Body | Status Codes |
|---|---|---|---|---|---|
| **GET** | `/` | Other | Home | No | 200 |
| **GET** | `/api/activity-logs` | Activity Logs | Activity Logs | No | 200, 422 |
| **GET** | `/api/activity-logs/` | Activity Logs | Activity Logs | No | 200, 422 |
| **GET** | `/api/activity-logs/export` | Activity Logs | Export Logs | No | 200 |
| **GET** | `/api/admin/affiliate-payouts` | Affiliate Payouts | Admin List Payouts | No | 200, 422 |
| **GET** | `/api/admin/messages/booking-conversations/{booking_id}` | Admin Messaging | Booking Conversations For Admin | No | 200, 422 |
| **POST** | `/api/admin/messages/booking-conversations/{conversation_id}/messages` | Admin Messaging | Booking Conversation Reply As Admin | Yes | 200, 422 |
| **GET** | `/api/admin/messages/conversations` | Admin Messaging | Conversations | No | 200, 422 |
| **GET** | `/api/admin/messages/conversations/{conversation_id}` | Admin Messaging | Conversation Thread | No | 200, 422 |
| **POST** | `/api/admin/messages/conversations/{conversation_id}/messages` | Admin Messaging | Reply | Yes | 200, 422 |
| **GET** | `/api/admin/messages/unread-summary` | Admin Messaging | Unread Summary | No | 200 |
| **GET** | `/api/admin/permissions/` | Permissions | List Permissions | No | 200, 422 |
| **POST** | `/api/admin/permissions/` | Permissions | Add Permission | Yes | 200, 422 |
| **DELETE** | `/api/admin/permissions/{permission_id}` | Permissions | Remove Permission | No | 200, 422 |
| **GET** | `/api/admin/permissions/{permission_id}` | Permissions | Detail Permission | No | 200, 422 |
| **PUT** | `/api/admin/permissions/{permission_id}` | Permissions | Edit Permission | Yes | 200, 422 |
| **GET** | `/api/admin/reviews` | Reviews | List Reviews | No | 200, 422 |
| **PATCH** | `/api/admin/reviews/{review_id}/approve` | Reviews | Approve Review | No | 200, 422 |
| **PATCH** | `/api/admin/reviews/{review_id}/reject` | Reviews | Reject Review | No | 200, 422 |
| **GET** | `/api/admin/roles/` | Roles | List Roles | No | 200, 422 |
| **POST** | `/api/admin/roles/` | Roles | Add Role | Yes | 200, 422 |
| **GET** | `/api/admin/roles/public/options` | Roles | Public Role Options | No | 200 |
| **DELETE** | `/api/admin/roles/{role_id}` | Roles | Remove Role | No | 200, 422 |
| **GET** | `/api/admin/roles/{role_id}` | Roles | Detail Role | No | 200, 422 |
| **PUT** | `/api/admin/roles/{role_id}` | Roles | Edit Role | Yes | 200, 422 |
| **GET** | `/api/admin/roles/{role_id}/permissions` | Roles | Role Permissions | No | 200, 422 |
| **POST** | `/api/admin/roles/{role_id}/permissions` | Roles | Assign Permissions | Yes | 200, 422 |
| **POST** | `/api/admin/seed/geo` | Geo Seed | Trigger Geo Seed | No | 200, 422 |
| **GET** | `/api/admin/seed/geo/status` | Geo Seed | Geo Seed Status | No | 200 |
| **GET** | `/api/affiliate-commission-rules` | Affiliate Commission Rules | List Rules | No | 200, 422 |
| **POST** | `/api/affiliate-commission-rules` | Affiliate Commission Rules | Create Rule | Yes | 200, 422 |
| **GET** | `/api/affiliate-commission-rules/` | Affiliate Commission Rules | List Rules | No | 200, 422 |
| **POST** | `/api/affiliate-commission-rules/` | Affiliate Commission Rules | Create Rule | Yes | 200, 422 |
| **DELETE** | `/api/affiliate-commission-rules/{rule_id}` | Affiliate Commission Rules | Delete Rule | No | 200, 422 |
| **GET** | `/api/affiliate-commission-rules/{rule_id}` | Affiliate Commission Rules | Rule Detail | No | 200, 422 |
| **PUT** | `/api/affiliate-commission-rules/{rule_id}` | Affiliate Commission Rules | Update Rule | Yes | 200, 422 |
| **GET** | `/api/affiliate-links` | Affiliate Links (Admin) | List Links | No | 200, 422 |
| **POST** | `/api/affiliate-links` | Affiliate Links (Admin) | Create Link | Yes | 200, 422 |
| **GET** | `/api/affiliate-links/` | Affiliate Links (Admin) | List Links | No | 200, 422 |
| **POST** | `/api/affiliate-links/` | Affiliate Links (Admin) | Create Link | Yes | 200, 422 |
| **DELETE** | `/api/affiliate-links/{link_id}` | Affiliate Links (Admin) | Delete Link | No | 200, 422 |
| **GET** | `/api/affiliate-links/{link_id}` | Affiliate Links (Admin) | Link Detail | No | 200, 422 |
| **PUT** | `/api/affiliate-links/{link_id}` | Affiliate Links (Admin) | Update Link | Yes | 200, 422 |
| **POST** | `/api/affiliate-links/{link_id}/activate` | Affiliate Links (Admin) | Activate Link | No | 200, 422 |
| **POST** | `/api/affiliate-links/{link_id}/disable` | Affiliate Links (Admin) | Disable Link | No | 200, 422 |
| **POST** | `/api/affiliate-links/{link_id}/duplicate` | Affiliate Links (Admin) | Duplicate Link | No | 200, 422 |
| **GET** | `/api/affiliate-payouts` | Affiliate Tracking | List Payouts | No | 200, 422 |
| **POST** | `/api/affiliate-payouts` | Affiliate Tracking | Create Payout | Yes | 200, 422 |
| **POST** | `/api/affiliate-payouts/{payout_id}/approve` | Affiliate Payouts | Approve Payout | No | 200, 422 |
| **POST** | `/api/affiliate-payouts/{payout_id}/mark-paid` | Affiliate Payouts | Mark Paid | Yes | 200, 422 |
| **POST** | `/api/affiliate-payouts/{payout_id}/processing` | Affiliate Payouts | Mark Processing | No | 200, 422 |
| **POST** | `/api/affiliate-payouts/{payout_id}/reject` | Affiliate Payouts | Reject Payout | Yes | 200, 422 |
| **GET** | `/api/affiliate/messages` | Affiliate Tracking | Affiliate Messages | No | 200 |
| **POST** | `/api/affiliate/messages` | Affiliate Tracking | Send Affiliate Message | Yes | 200, 422 |
| **GET** | `/api/affiliate/payout-methods` | Affiliate Payouts | List Payout Methods | No | 200 |
| **POST** | `/api/affiliate/payout-methods` | Affiliate Payouts | Create Payout Method | Yes | 200, 422 |
| **DELETE** | `/api/affiliate/payout-methods/{method_id}` | Affiliate Payouts | Delete Payout Method | No | 200, 422 |
| **PUT** | `/api/affiliate/payout-methods/{method_id}` | Affiliate Payouts | Update Payout Method | Yes | 200, 422 |
| **POST** | `/api/affiliate/payout-requests` | Affiliate Payouts | Request Payout | Yes | 200, 422 |
| **GET** | `/api/affiliate/wallet` | Affiliate Payouts | Wallet Summary | No | 200 |
| **GET** | `/api/affiliate/wallet/transactions` | Affiliate Payouts | Wallet Transactions | No | 200, 422 |
| **GET** | `/api/affiliates` | Affiliates | Affiliates | No | 200, 422 |
| **POST** | `/api/affiliates` | Affiliates | Add Affiliate | Yes | 200, 422 |
| **GET** | `/api/affiliates/` | Affiliates | Affiliates | No | 200, 422 |
| **POST** | `/api/affiliates/` | Affiliates | Add Affiliate | Yes | 200, 422 |
| **GET** | `/api/affiliates/document-requirements` | Affiliates | Affiliate Document Requirements | No | 200 |
| **GET** | `/api/affiliates/me` | Affiliates | My Affiliate | No | 200 |
| **PATCH** | `/api/affiliates/me` | Affiliates | Edit My Affiliate | Yes | 200, 422 |
| **PUT** | `/api/affiliates/me` | Affiliates | Edit My Affiliate | Yes | 200, 422 |
| **POST** | `/api/affiliates/me/accept-commission` | Affiliates | Accept My Commission | No | 200 |
| **POST** | `/api/affiliates/me/bank-details/edit-request` | Affiliates | Request My Bank Detail Edit | No | 200 |
| **POST** | `/api/affiliates/submit-verification` | Affiliates | Submit My Verification | No | 200 |
| **GET** | `/api/affiliates/track/{ref_code}` | Affiliate Tracking | Track Click | No | 200, 422 |
| **GET** | `/api/affiliates/{affiliate_id}` | Affiliates | Affiliate Detail | No | 200, 422 |
| **PUT** | `/api/affiliates/{affiliate_id}` | Affiliates | Edit Affiliate | Yes | 200, 422 |
| **POST** | `/api/affiliates/{affiliate_id}/activate` | Affiliates | Activate | No | 200, 422 |
| **PATCH** | `/api/affiliates/{affiliate_id}/api-link` | Affiliates | Api Link | Yes | 200, 422 |
| **PATCH** | `/api/affiliates/{affiliate_id}/approve` | Affiliates | Approve | No | 200, 422 |
| **POST** | `/api/affiliates/{affiliate_id}/bank-details/reject` | Affiliates | Reject Bank Detail Edit | Yes | 200, 422 |
| **POST** | `/api/affiliates/{affiliate_id}/bank-details/unlock` | Affiliates | Unlock Bank Detail Edit | No | 200, 422 |
| **GET** | `/api/affiliates/{affiliate_id}/clicks` | Affiliate Tracking | List Clicks | No | 200, 422 |
| **GET** | `/api/affiliates/{affiliate_id}/commission-calculator` | Affiliates | Affiliate Commission Calculator | No | 200, 422 |
| **GET** | `/api/affiliates/{affiliate_id}/commissions` | Affiliate Tracking | Get Commissions | No | 200, 422 |
| **GET** | `/api/affiliates/{affiliate_id}/conversions` | Affiliate Tracking | List Conversions | No | 200, 422 |
| **GET** | `/api/affiliates/{affiliate_id}/documents` | Affiliates | Get Affiliate Documents | No | 200, 422 |
| **POST** | `/api/affiliates/{affiliate_id}/documents` | Affiliates | Upload Affiliate Document | Yes | 200, 422 |
| **PATCH** | `/api/affiliates/{affiliate_id}/documents/{document_id}/review` | Affiliates | Review Document | Yes | 200, 422 |
| **GET** | `/api/affiliates/{affiliate_id}/links` | Affiliate Tracking | List Links | No | 200, 422 |
| **POST** | `/api/affiliates/{affiliate_id}/links` | Affiliate Tracking | Create Link | Yes | 200, 422 |
| **GET** | `/api/affiliates/{affiliate_id}/links/{link_id}` | Affiliate Tracking | Link Detail | No | 200, 422 |
| **PUT** | `/api/affiliates/{affiliate_id}/links/{link_id}` | Affiliate Tracking | Update Own Link | Yes | 200, 422 |
| **PATCH** | `/api/affiliates/{affiliate_id}/reject` | Affiliates | Reject | Yes | 200, 422 |
| **POST** | `/api/affiliates/{affiliate_id}/suspend` | Affiliates | Suspend | Yes | 200, 422 |
| **GET** | `/api/agent-ledgers` | Agent Ledger | List Ledgers | No | 200, 422 |
| **GET** | `/api/agent-payouts` | Agent Ledger | List Payouts | No | 200, 422 |
| **POST** | `/api/agent-payouts` | Agent Ledger | Create Payout | Yes | 200, 422 |
| **POST** | `/api/agent-payouts/{payout_id}/approve` | Agent Ledger | Approve Payout | No | 200, 422 |
| **PATCH** | `/api/agent-payouts/{payout_id}/mark-paid` | Agent Ledger | Mark Paid | Yes | 200, 422 |
| **POST** | `/api/agent-payouts/{payout_id}/mark-paid` | Agent Ledger | Mark Paid Post | No | 200, 422 |
| **POST** | `/api/agent-payouts/{payout_id}/reject` | Agent Ledger | Reject Payout | Yes | 200, 422 |
| **GET** | `/api/agent-statements/{agent_id}` | Agent Ledger | Agent Statement | No | 200, 422 |
| **GET** | `/api/agent/messages` | Agent Portal | Agent Messages | No | 200 |
| **POST** | `/api/agent/messages` | Agent Portal | Send Agent Message | Yes | 200, 422 |
| **GET** | `/api/agents` | Agents | Agents | No | 200, 422 |
| **POST** | `/api/agents` | Agents | Add Agent | Yes | 200, 422 |
| **GET** | `/api/agents/` | Agents | Agents | No | 200, 422 |
| **POST** | `/api/agents/` | Agents | Add Agent | Yes | 200, 422 |
| **POST** | `/api/agents/bulk-approve` | Agents | Bulk Approve | Yes | 200, 422 |
| **POST** | `/api/agents/bulk-reject` | Agents | Bulk Reject | Yes | 200, 422 |
| **GET** | `/api/agents/document-requirements` | Agents | Document Requirements | No | 200 |
| **GET** | `/api/agents/export` | Agents | Export Agents Endpoint | No | 200 |
| **GET** | `/api/agents/me` | Agents | My Agent | No | 200 |
| **PATCH** | `/api/agents/me` | Agents | Edit My Agent | Yes | 200, 422 |
| **PUT** | `/api/agents/me` | Agents | Edit My Agent | Yes | 200, 422 |
| **POST** | `/api/agents/me/accept-commission` | Agents | Accept My Commission | No | 200 |
| **POST** | `/api/agents/me/bank-details/edit-request` | Agents | Request My Bank Detail Edit | No | 200 |
| **GET** | `/api/agents/me/commission-calculator` | Agents | My Commission Calculator | No | 200, 422 |
| **POST** | `/api/agents/me/commission-request` | Agents | Request My Commission | Yes | 200, 422 |
| **GET** | `/api/agents/pending` | Agents | Pending Agents | No | 200, 422 |
| **POST** | `/api/agents/register` | Agents | Register Agent | Yes | 200, 422 |
| **POST** | `/api/agents/submit-verification` | Agents | Submit Verification | No | 200 |
| **POST** | `/api/agents/verify-email` | Agents | Verify Agent Email | Yes | 200, 422 |
| **GET** | `/api/agents/{agent_id}` | Agents | Agent Detail | No | 200, 422 |
| **PATCH** | `/api/agents/{agent_id}` | Agents | Edit Agent | Yes | 200, 422 |
| **PUT** | `/api/agents/{agent_id}` | Agents | Edit Agent | Yes | 200, 422 |
| **PATCH** | `/api/agents/{agent_id}/approve` | Agents | Approve | No | 200, 422 |
| **POST** | `/api/agents/{agent_id}/approve` | Agents | Approve | No | 200, 422 |
| **POST** | `/api/agents/{agent_id}/bank-details/reject` | Agents | Reject Bank Detail Edit | Yes | 200, 422 |
| **POST** | `/api/agents/{agent_id}/bank-details/unlock` | Agents | Unlock Bank Detail Edit | No | 200, 422 |
| **POST** | `/api/agents/{agent_id}/commission-request/reject` | Agents | Reject Commission Request | No | 200, 422 |
| **PATCH** | `/api/agents/{agent_id}/discount` | Agents | Discount | Yes | 200, 422 |
| **POST** | `/api/agents/{agent_id}/discount` | Agents | Discount | Yes | 200, 422 |
| **GET** | `/api/agents/{agent_id}/documents` | Agents | Get Agent Documents | No | 200, 422 |
| **POST** | `/api/agents/{agent_id}/documents` | Agents | Upload Agent Document | Yes | 200, 422 |
| **PATCH** | `/api/agents/{agent_id}/documents/{document_id}/review` | Agents | Review Document | Yes | 200, 422 |
| **GET** | `/api/agents/{agent_id}/ledger` | Agent Ledger | Agent Ledger | No | 200, 422 |
| **PATCH** | `/api/agents/{agent_id}/partial-approve` | Agents | Partial Approve | Yes | 200, 422 |
| **POST** | `/api/agents/{agent_id}/partial-approve` | Agents | Partial Approve | Yes | 200, 422 |
| **PATCH** | `/api/agents/{agent_id}/reject` | Agents | Reject | Yes | 200, 422 |
| **POST** | `/api/agents/{agent_id}/reject` | Agents | Reject | Yes | 200, 422 |
| **POST** | `/api/agents/{agent_id}/request-correction` | Agents | Request Correction | Yes | 200, 422 |
| **GET** | `/api/audit-logs` | Activity Logs | Activity Logs | No | 200, 422 |
| **GET** | `/api/audit-logs/` | Activity Logs | Activity Logs | No | 200, 422 |
| **GET** | `/api/audit-logs/export` | Activity Logs | Export Logs | No | 200 |
| **POST** | `/api/auth/2fa/disable` | Authentication | Two Factor Disable | Yes | 200, 422 |
| **POST** | `/api/auth/2fa/enable` | Authentication | Two Factor Enable | Yes | 200, 422 |
| **POST** | `/api/auth/2fa/login-verify` | Authentication | Two Factor Login Verify | Yes | 200, 422 |
| **POST** | `/api/auth/2fa/setup` | Authentication | Two Factor Setup | No | 200 |
| **GET** | `/api/auth/account-status` | Authentication | Account Status | No | 200 |
| **POST** | `/api/auth/change-registration-email` | Authentication | Change Email | Yes | 200, 422 |
| **POST** | `/api/auth/complete-registration` | Authentication | Complete Registration Request | Yes | 200, 422 |
| **POST** | `/api/auth/create-password` | Authentication | Create Registration Password | Yes | 200, 422 |
| **POST** | `/api/auth/force-logout` | Authentication | Force Logout | Yes | 200, 422 |
| **POST** | `/api/auth/forgot-password` | Authentication | Forgot Password Request | Yes | 200, 422 |
| **GET** | `/api/auth/google` | Google Authentication | Google Login | No | 200, 422 |
| **GET** | `/api/auth/google/callback` | Google Authentication | Google Callback | No | 200, 422 |
| **POST** | `/api/auth/login` | Authentication | Login | Yes | 200, 422 |
| **GET** | `/api/auth/login-history` | Authentication | Login History | No | 200, 422 |
| **POST** | `/api/auth/logout` | Authentication | Logout | No | 200 |
| **POST** | `/api/auth/logout-all` | Authentication | Logout All | No | 200 |
| **GET** | `/api/auth/me` | Authentication | Current Session | No | 200 |
| **GET** | `/api/auth/oauth/providers` | Social Authentication | Provider Status | No | 200 |
| **GET** | `/api/auth/oauth/{provider}/start` | Social Authentication | Start Social Auth | No | 200, 422 |
| **POST** | `/api/auth/otp/request` | Authentication | Otp Request | Yes | 200, 422 |
| **POST** | `/api/auth/otp/verify` | Authentication | Otp Verify | Yes | 200, 422 |
| **POST** | `/api/auth/refresh` | Authentication | Refresh | Yes | 200, 422 |
| **POST** | `/api/auth/refresh-token` | Authentication | Refresh Token | Yes | 200, 422 |
| **POST** | `/api/auth/register` | Authentication | Register | Yes | 200, 422 |
| **POST** | `/api/auth/register/agent` | Authentication | Register Agent | Yes | 200, 422 |
| **POST** | `/api/auth/register/customer` | Authentication | Register Customer | Yes | 200, 422 |
| **POST** | `/api/auth/register/supplier` | Authentication | Register Supplier | Yes | 200, 422 |
| **POST** | `/api/auth/resend-verification` | Authentication | Resend Verification | Yes | 200, 422 |
| **POST** | `/api/auth/reset-password` | Authentication | Reset Password Request | Yes | 200, 422 |
| **GET** | `/api/auth/reset-password/validate` | Authentication | Validate Reset Password Link | No | 200, 422 |
| **GET** | `/api/auth/verify-email` | Authentication | Verify Email Link | No | 200, 422 |
| **POST** | `/api/auth/verify-email` | Authentication | Verify Email Request | Yes | 200, 422 |
| **GET** | `/api/auth/verify-email/validate` | Authentication | Validate Verification Link | No | 200, 422 |
| **GET** | `/api/bookings` | Bookings | List Bookings | No | 200, 422 |
| **POST** | `/api/bookings` | Bookings | Add Booking | Yes | 200, 422 |
| **GET** | `/api/bookings/` | Bookings | List Bookings | No | 200, 422 |
| **POST** | `/api/bookings/` | Bookings | Add Booking | Yes | 200, 422 |
| **POST** | `/api/bookings/calculate-price` | Bookings | Calculate Price | Yes | 200, 422 |
| **POST** | `/api/bookings/communications/{communication_id}/replies` | Bookings | Reply Booking Communication | Yes | 200, 422 |
| **POST** | `/api/bookings/expire-stale` | Bookings | Expire Stale Bookings Endpoint | No | 200, 422 |
| **GET** | `/api/bookings/export` | Bookings | Export Bookings Endpoint | No | 200 |
| **GET** | `/api/bookings/upcoming` | Bookings | Upcoming Bookings | No | 200 |
| **GET** | `/api/bookings/{booking_id}` | Bookings | Booking Detail | No | 200, 422 |
| **PUT** | `/api/bookings/{booking_id}` | Bookings | Edit Booking | Yes | 200, 422 |
| **POST** | `/api/bookings/{booking_id}/assign-supplier` | Bookings | Assign Supplier Endpoint | Yes | 200, 422 |
| **GET** | `/api/bookings/{booking_id}/calendar-event` | Booking Calendar | Get Calendar Event | No | 200, 422 |
| **GET** | `/api/bookings/{booking_id}/calendar-event/download` | Booking Calendar | Download Ics | No | 200, 422 |
| **POST** | `/api/bookings/{booking_id}/calendar-sync` | Booking Calendar | Sync Calendar | No | 200, 422 |
| **PATCH** | `/api/bookings/{booking_id}/cancel` | Bookings | Cancel Booking Endpoint | Yes | 200, 422 |
| **POST** | `/api/bookings/{booking_id}/cancel-request` | Cancellations | Customer Cancel Request | Yes | 200, 422 |
| **PATCH** | `/api/bookings/{booking_id}/cancellation-request/approve` | Cancellations | Approve Booking Cancellation | Yes | 200, 422 |
| **PATCH** | `/api/bookings/{booking_id}/cancellation-request/reject` | Cancellations | Reject Booking Cancellation | Yes | 200, 422 |
| **POST** | `/api/bookings/{booking_id}/communications` | Bookings | Create Booking Communication | Yes | 200, 422 |
| **GET** | `/api/bookings/{booking_id}/conversation` | Booking Messaging | Booking Conversation Thread | No | 200, 422 |
| **POST** | `/api/bookings/{booking_id}/conversation/messages` | Booking Messaging | Send Booking Conversation Message | Yes | 200, 422 |
| **POST** | `/api/bookings/{booking_id}/hide-from-agent` | Bookings | Hide From Agent Bookings | No | 200, 422 |
| **GET** | `/api/bookings/{booking_id}/modifications` | Bookings | Booking Modifications | No | 200, 422 |
| **POST** | `/api/bookings/{booking_id}/modifications` | Bookings | Request Booking Modification | Yes | 200, 422 |
| **POST** | `/api/bookings/{booking_id}/modifications/{modification_id}/approve` | Bookings | Approve Booking Modification | Yes | 200, 422 |
| **POST** | `/api/bookings/{booking_id}/modifications/{modification_id}/reject` | Bookings | Reject Booking Modification | Yes | 200, 422 |
| **GET** | `/api/bookings/{booking_id}/payment-link` | Bookings | Booking Payment Link | No | 200, 422 |
| **PATCH** | `/api/bookings/{booking_id}/status` | Bookings | Change Booking Status | Yes | 200, 422 |
| **GET** | `/api/bookings/{booking_id}/status-history` | Bookings | Booking Status History | No | 200, 422 |
| **PATCH** | `/api/bookings/{booking_id}/travel-date` | Bookings | Change Booking Travel Date | Yes | 200, 422 |
| **GET** | `/api/cancellations` | Cancellations | List Cancellations | No | 200, 422 |
| **PATCH** | `/api/cancellations/{request_id}/approve` | Cancellations | Approve Cancellation | Yes | 200, 422 |
| **POST** | `/api/cancellations/{request_id}/process-refund` | Cancellations | Process Refund | Yes | 200, 422 |
| **PATCH** | `/api/cancellations/{request_id}/reject` | Cancellations | Reject Cancellation | Yes | 200, 422 |
| **GET** | `/api/chatbot/admin/analytics` | Chatbot | Admin Analytics | No | 200, 422 |
| **GET** | `/api/chatbot/admin/faqs` | Chatbot | Admin List Faqs | No | 200, 422 |
| **POST** | `/api/chatbot/admin/faqs` | Chatbot | Admin Create Faq | Yes | 201, 422 |
| **DELETE** | `/api/chatbot/admin/faqs/{faq_id}` | Chatbot | Admin Delete Faq | No | 204, 422 |
| **PUT** | `/api/chatbot/admin/faqs/{faq_id}` | Chatbot | Admin Update Faq | Yes | 200, 422 |
| **POST** | `/api/chatbot/admin/reindex` | Chatbot | Admin Reindex | No | 200 |
| **GET** | `/api/chatbot/admin/sessions` | Chatbot | Admin List Sessions | No | 200, 422 |
| **GET** | `/api/chatbot/admin/sessions/{session_id}/messages` | Chatbot | Admin Session Messages | No | 200, 422 |
| **POST** | `/api/chatbot/chat` | Chatbot | Chat | Yes | 200, 422 |
| **GET** | `/api/chatbot/faqs` | Chatbot | Public Faqs | No | 200 |
| **POST** | `/api/chatbot/feedback` | Chatbot | Submit Chat Feedback | Yes | 200, 422 |
| **GET** | `/api/chatbot/health` | Chatbot | Chatbot Health | No | 200 |
| **GET** | `/api/checkout/admin/sessions` | Checkout | Admin List Checkout Sessions | No | 200, 422 |
| **GET** | `/api/checkout/session/{session_key}` | Checkout | Get Checkout Session | No | 200, 422 |
| **PATCH** | `/api/checkout/session/{session_key}` | Checkout | Update Checkout Session | Yes | 200, 422 |
| **POST** | `/api/checkout/session/{session_key}/confirm` | Checkout | Confirm Checkout | Yes | 200, 422 |
| **POST** | `/api/checkout/start` | Checkout | Start Checkout | Yes | 200, 422 |
| **GET** | `/api/cities` | CMS | Cities | No | 200, 422 |
| **POST** | `/api/cities` | CMS | Add City | Yes | 200, 422 |
| **GET** | `/api/cities/{city_id}` | CMS | City Detail | No | 200, 422 |
| **PUT** | `/api/cities/{city_id}` | CMS | Edit City | Yes | 200, 422 |
| **PATCH** | `/api/cities/{city_id}/status` | CMS | City Status | Yes | 200, 422 |
| **GET** | `/api/client/config` | Client | Client Config | No | 200 |
| **GET** | `/api/client/tours` | Client | Public Tours | No | 200, 422 |
| **GET** | `/api/client/tours/{tour_id}` | Client | Public Tour Detail | No | 200, 422 |
| **GET** | `/api/client/tours/{tour_id}/calendar` | Client | Public Tour Calendar | No | 200, 422 |
| **GET** | `/api/client/tours/{tour_id}/exclusions` | Client | Public Tour Exclusions | No | 200, 422 |
| **GET** | `/api/client/tours/{tour_id}/gallery` | Client | Public Tour Gallery | No | 200, 422 |
| **GET** | `/api/client/tours/{tour_id}/highlights` | Client | Public Tour Highlights | No | 200, 422 |
| **GET** | `/api/client/tours/{tour_id}/inclusions` | Client | Public Tour Inclusions | No | 200, 422 |
| **GET** | `/api/client/tours/{tour_id}/itineraries` | Client | Public Tour Itineraries | No | 200, 422 |
| **GET** | `/api/client/tours/{tour_id}/optional-activities` | Client | Public Tour Activities | No | 200, 422 |
| **GET** | `/api/client/tours/{tour_id}/overview` | Client | Public Tour Overview | No | 200, 422 |
| **GET** | `/api/client/tours/{tour_id}/pricing` | Client | Public Tour Pricing | No | 200, 422 |
| **GET** | `/api/client/tours/{tour_id}/similar-tours` | Client | Public Tour Similar Tours | No | 200, 422 |
| **GET** | `/api/cms/blogs` | Website CMS | List Blogs | No | 200, 422 |
| **POST** | `/api/cms/blogs` | Website CMS | Create Blog | Yes | 200, 422 |
| **DELETE** | `/api/cms/blogs/{item_id}` | Website CMS | Delete Blog | No | 200, 422 |
| **GET** | `/api/cms/blogs/{item_id}` | Website CMS | Get Blog | No | 200, 422 |
| **PUT** | `/api/cms/blogs/{item_id}` | Website CMS | Update Blog | Yes | 200, 422 |
| **GET** | `/api/cms/content-blocks/{key}` | Website CMS | Get Content Block | No | 200, 422 |
| **PUT** | `/api/cms/content-blocks/{key}` | Website CMS | Upsert Content Block | Yes | 200, 422 |
| **GET** | `/api/cms/country-pages` | Website CMS | List Country Pages | No | 200, 422 |
| **POST** | `/api/cms/country-pages` | Website CMS | Create Country Page | Yes | 200, 422 |
| **DELETE** | `/api/cms/country-pages/{item_id}` | Website CMS | Delete Country Page | No | 200, 422 |
| **PUT** | `/api/cms/country-pages/{item_id}` | Website CMS | Update Country Page | Yes | 200, 422 |
| **GET** | `/api/cms/customer-reviews` | Website CMS | List Reviews | No | 200, 422 |
| **POST** | `/api/cms/customer-reviews` | Website CMS | Create Review | Yes | 200, 422 |
| **DELETE** | `/api/cms/customer-reviews/{item_id}` | Website CMS | Delete Review | No | 200, 422 |
| **PUT** | `/api/cms/customer-reviews/{item_id}` | Website CMS | Update Review | Yes | 200, 422 |
| **GET** | `/api/cms/external-links` | Website CMS | List Links | No | 200, 422 |
| **POST** | `/api/cms/external-links` | Website CMS | Create Link | Yes | 200, 422 |
| **DELETE** | `/api/cms/external-links/{item_id}` | Website CMS | Delete Link | No | 200, 422 |
| **PUT** | `/api/cms/external-links/{item_id}` | Website CMS | Update Link | Yes | 200, 422 |
| **GET** | `/api/cms/favourite-countries` | Website CMS | List Favourite Countries | No | 200, 422 |
| **POST** | `/api/cms/favourite-countries` | Website CMS | Create Favourite Country | Yes | 200, 422 |
| **DELETE** | `/api/cms/favourite-countries/{item_id}` | Website CMS | Delete Favourite Country | No | 200, 422 |
| **PUT** | `/api/cms/favourite-countries/{item_id}` | Website CMS | Update Favourite Country | Yes | 200, 422 |
| **GET** | `/api/cms/footer` | Website CMS | Public Footer | No | 200 |
| **GET** | `/api/cms/footer-links` | Website CMS | List Footer Links | No | 200, 422 |
| **POST** | `/api/cms/footer-links` | Website CMS | Create Footer Link | Yes | 200, 422 |
| **DELETE** | `/api/cms/footer-links/{item_id}` | Website CMS | Delete Footer Link | No | 200, 422 |
| **PUT** | `/api/cms/footer-links/{item_id}` | Website CMS | Update Footer Link | Yes | 200, 422 |
| **GET** | `/api/cms/footer-sections` | Website CMS | List Footer Sections | No | 200, 422 |
| **POST** | `/api/cms/footer-sections` | Website CMS | Create Footer Section | Yes | 200, 422 |
| **DELETE** | `/api/cms/footer-sections/{item_id}` | Website CMS | Delete Footer Section | No | 200, 422 |
| **PUT** | `/api/cms/footer-sections/{item_id}` | Website CMS | Update Footer Section | Yes | 200, 422 |
| **GET** | `/api/cms/handpicked-tours` | Website CMS | List Handpicked Tours | No | 200, 422 |
| **POST** | `/api/cms/handpicked-tours` | Website CMS | Create Handpicked Tour | Yes | 200, 422 |
| **DELETE** | `/api/cms/handpicked-tours/{item_id}` | Website CMS | Delete Handpicked Tour | No | 200, 422 |
| **PUT** | `/api/cms/handpicked-tours/{item_id}` | Website CMS | Update Handpicked Tour | Yes | 200, 422 |
| **GET** | `/api/cms/help-centre` | Website CMS | List Help | No | 200, 422 |
| **POST** | `/api/cms/help-centre` | Website CMS | Create Help | Yes | 200, 422 |
| **DELETE** | `/api/cms/help-centre/{item_id}` | Website CMS | Delete Help | No | 200, 422 |
| **PUT** | `/api/cms/help-centre/{item_id}` | Website CMS | Update Help | Yes | 200, 422 |
| **GET** | `/api/cms/homepage-banners` | Website CMS | List Banners | No | 200, 422 |
| **POST** | `/api/cms/homepage-banners` | Website CMS | Create Banner | Yes | 200, 422 |
| **DELETE** | `/api/cms/homepage-banners/{item_id}` | Website CMS | Delete Banner | No | 200, 422 |
| **PUT** | `/api/cms/homepage-banners/{item_id}` | Website CMS | Update Banner | Yes | 200, 422 |
| **GET** | `/api/cms/pages` | Website CMS | List Cms Pages | No | 200, 422 |
| **POST** | `/api/cms/pages` | Website CMS | Create Cms Page | Yes | 200, 422 |
| **GET** | `/api/cms/pages/by-slug/{slug}` | Website CMS | Public Cms Page | No | 200, 422 |
| **DELETE** | `/api/cms/pages/{item_id}` | Website CMS | Delete Cms Page | No | 200, 422 |
| **PUT** | `/api/cms/pages/{item_id}` | Website CMS | Update Cms Page | Yes | 200, 422 |
| **GET** | `/api/cms/policies` | Website CMS | List Policies | No | 200, 422 |
| **PUT** | `/api/cms/policies` | Website CMS | Upsert Policy | Yes | 200, 422 |
| **GET** | `/api/cms/policies/{slug}` | Website CMS | Get Policy | No | 200, 422 |
| **GET** | `/api/cms/popular-destinations` | Website CMS | List Destinations | No | 200, 422 |
| **POST** | `/api/cms/popular-destinations` | Website CMS | Create Destination | Yes | 200, 422 |
| **DELETE** | `/api/cms/popular-destinations/{item_id}` | Website CMS | Delete Destination | No | 200, 422 |
| **PUT** | `/api/cms/popular-destinations/{item_id}` | Website CMS | Update Destination | Yes | 200, 422 |
| **GET** | `/api/cms/popular-tours` | Website CMS | List Popular Tours | No | 200, 422 |
| **POST** | `/api/cms/popular-tours` | Website CMS | Create Popular Tour | Yes | 200, 422 |
| **DELETE** | `/api/cms/popular-tours/{item_id}` | Website CMS | Delete Popular Tour | No | 200, 422 |
| **PUT** | `/api/cms/popular-tours/{item_id}` | Website CMS | Update Popular Tour | Yes | 200, 422 |
| **GET** | `/api/cms/promotional-popups` | Website CMS | List Popups | No | 200, 422 |
| **POST** | `/api/cms/promotional-popups` | Website CMS | Create Popup | Yes | 200, 422 |
| **DELETE** | `/api/cms/promotional-popups/{item_id}` | Website CMS | Delete Popup | No | 200, 422 |
| **PUT** | `/api/cms/promotional-popups/{item_id}` | Website CMS | Update Popup | Yes | 200, 422 |
| **GET** | `/api/cms/sitemap` | Website CMS | List Sitemap Entries | No | 200, 422 |
| **POST** | `/api/cms/sitemap` | Website CMS | Create Sitemap Entry | Yes | 200, 422 |
| **GET** | `/api/cms/sitemap.xml` | Website CMS | Get Sitemap Xml | No | 200 |
| **DELETE** | `/api/cms/sitemap/{item_id}` | Website CMS | Delete Sitemap Entry | No | 200, 422 |
| **PUT** | `/api/cms/sitemap/{item_id}` | Website CMS | Update Sitemap Entry | Yes | 200, 422 |
| **GET** | `/api/cms/tours-on-deals` | Website CMS | List Deals | No | 200, 422 |
| **POST** | `/api/cms/tours-on-deals` | Website CMS | Create Deal | Yes | 200, 422 |
| **DELETE** | `/api/cms/tours-on-deals/{item_id}` | Website CMS | Delete Deal | No | 200, 422 |
| **PUT** | `/api/cms/tours-on-deals/{item_id}` | Website CMS | Update Deal | Yes | 200, 422 |
| **GET** | `/api/countries` | CMS | Countries | No | 200, 422 |
| **POST** | `/api/countries` | CMS | Add Country | Yes | 200, 422 |
| **PATCH** | `/api/countries/bulk-disable` | CMS | Bulk Disable Countries | No | 200, 422 |
| **GET** | `/api/countries/{country_id}` | CMS | Country Detail | No | 200, 422 |
| **PUT** | `/api/countries/{country_id}` | CMS | Edit Country | Yes | 200, 422 |
| **PATCH** | `/api/countries/{country_id}/status` | CMS | Country Status | Yes | 200, 422 |
| **GET** | `/api/currencies` | CMS | Currencies | No | 200, 422 |
| **POST** | `/api/currencies` | CMS | Add Currency | Yes | 200, 422 |
| **GET** | `/api/currencies/{currency_id}` | CMS | Currency Detail | No | 200, 422 |
| **PUT** | `/api/currencies/{currency_id}` | CMS | Edit Currency | Yes | 200, 422 |
| **PATCH** | `/api/currencies/{currency_id}/status` | CMS | Currency Status | Yes | 200, 422 |
| **GET** | `/api/currency/admin/rates` | Currency | Admin Currency Rates | No | 200 |
| **POST** | `/api/currency/admin/refresh` | Currency | Admin Refresh Currency Rates | No | 200 |
| **GET** | `/api/currency/context` | Currency | Currency Context | No | 200, 422 |
| **GET** | `/api/currency/convert` | Currency | Currency Convert | No | 200, 422 |
| **GET** | `/api/currency/rates` | Currency | Currency Rates | No | 200, 422 |
| **GET** | `/api/customer/bookings` | Customer Portal | Customer Bookings | No | 200, 422 |
| **POST** | `/api/customer/bookings` | Customer Portal | Create Customer Booking | Yes | 200, 422 |
| **POST** | `/api/customer/bookings/calculate-price` | Customer Portal | Customer Calculate Price | Yes | 200, 422 |
| **GET** | `/api/customer/bookings/{booking_id}` | Customer Portal | Customer Booking Detail | No | 200, 422 |
| **POST** | `/api/customer/bookings/{booking_id}/cancel` | Customer Portal | Request Booking Cancellation | Yes | 200, 422 |
| **GET** | `/api/customer/bookings/{booking_id}/confirmation-receipt` | Customer Portal | Customer Booking Confirmation Receipt | No | 200, 422 |
| **GET** | `/api/customer/bookings/{booking_id}/itinerary` | Customer Portal | Customer Booking Itinerary | No | 200, 422 |
| **POST** | `/api/customer/bookings/{booking_id}/pay` | Customer Portal | Record Customer Manual Payment | Yes | 200, 422 |
| **POST** | `/api/customer/bookings/{booking_id}/remove-unpaid` | Customer Portal | Remove Unpaid Booking | No | 200, 422 |
| **GET** | `/api/customer/cancellations` | Customer Portal | Customer Cancellations | No | 200, 422 |
| **POST** | `/api/customer/change-password` | Customer Portal | Change Customer Password | Yes | 200, 422 |
| **GET** | `/api/customer/invoices` | Customer Portal | Customer Invoices | No | 200, 422 |
| **GET** | `/api/customer/invoices/{invoice_id}/download` | Customer Portal | Customer Invoice Download | No | 200, 422 |
| **GET** | `/api/customer/messages` | Customer Portal | Customer Messages | No | 200 |
| **POST** | `/api/customer/messages` | Customer Portal | Send Customer Portal Message | Yes | 200, 422 |
| **GET** | `/api/customer/payments` | Customer Portal | Customer Payments | No | 200, 422 |
| **GET** | `/api/customer/profile` | Customer Portal | Customer Profile | No | 200 |
| **PUT** | `/api/customer/profile` | Customer Portal | Update Customer Profile | Yes | 200, 422 |
| **POST** | `/api/customer/reviews` | Reviews | Submit Review | Yes | 200, 422 |
| **GET** | `/api/customer/reviews/eligibility/{booking_id}` | Reviews | Get Review Eligibility | No | 200, 422 |
| **PATCH** | `/api/customer/reviews/{review_id}` | Reviews | Update Review | Yes | 200, 422 |
| **GET** | `/api/customer/travellers` | Customer Portal | Customer Saved Travellers | No | 200 |
| **POST** | `/api/customer/travellers` | Customer Portal | Add Saved Traveller | Yes | 200, 422 |
| **DELETE** | `/api/customer/travellers/{traveller_id}` | Customer Portal | Delete Saved Traveller | No | 200, 422 |
| **PUT** | `/api/customer/travellers/{traveller_id}` | Customer Portal | Update Saved Traveller | Yes | 200, 422 |
| **GET** | `/api/customers` | Customers | List Customers | No | 200, 422 |
| **POST** | `/api/customers` | Customers | Add Customer | Yes | 200, 422 |
| **GET** | `/api/customers/` | Customers | List Customers | No | 200, 422 |
| **POST** | `/api/customers/` | Customers | Add Customer | Yes | 200, 422 |
| **POST** | `/api/customers/link` | Customers | Link Existing Customer | Yes | 200, 422 |
| **GET** | `/api/customers/me` | Customers | My Customer | No | 200 |
| **PATCH** | `/api/customers/me` | Customers | Edit My Customer | Yes | 200, 422 |
| **PUT** | `/api/customers/me` | Customers | Edit My Customer | Yes | 200, 422 |
| **POST** | `/api/customers/me/bookings` | Customers | Self Create Booking | Yes | 200, 422 |
| **GET** | `/api/customers/{customer_id}` | Customers | Customer Detail | No | 200, 422 |
| **PUT** | `/api/customers/{customer_id}` | Customers | Edit Customer | Yes | 200, 422 |
| **PATCH** | `/api/customers/{customer_id}/block` | Customers | Block Customer Account | Yes | 200, 422 |
| **POST** | `/api/customers/{customer_id}/block` | Customers | Block Customer Account Compat | Yes | 200, 422 |
| **GET** | `/api/customers/{customer_id}/bookings` | Customers | Customer Booking History | No | 200, 422 |
| **GET** | `/api/customers/{customer_id}/communications` | Customers | Customer Communication History | No | 200, 422 |
| **POST** | `/api/customers/{customer_id}/communications` | Customers | Send Customer Communication | Yes | 200, 422 |
| **GET** | `/api/customers/{customer_id}/payments` | Customers | Customer Payment History | No | 200, 422 |
| **POST** | `/api/customers/{customer_id}/reset-password` | Customers | Reset Customer Login Password | No | 200, 422 |
| **PATCH** | `/api/customers/{customer_id}/status` | Customers | Change Customer Status | Yes | 200, 422 |
| **PATCH** | `/api/customers/{customer_id}/unblock` | Customers | Unblock Customer Account | No | 200, 422 |
| **POST** | `/api/customers/{customer_id}/unblock` | Customers | Unblock Customer Account Compat | No | 200, 422 |
| **GET** | `/api/dashboard/alerts` | Dashboard | Dashboard Alerts | No | 200 |
| **GET** | `/api/dashboard/bookings` | Dashboard | Booking Analytics | No | 200, 422 |
| **GET** | `/api/dashboard/charts` | Dashboard | Dashboard Charts | No | 200, 422 |
| **GET** | `/api/dashboard/me` | Dashboard | My Dashboard | No | 200 |
| **GET** | `/api/dashboard/payments` | Dashboard | Payment Summary | No | 200, 422 |
| **GET** | `/api/dashboard/recent-activities` | Dashboard | Recent Activities | No | 200, 422 |
| **GET** | `/api/dashboard/revenue` | Dashboard | Revenue Analytics | No | 200, 422 |
| **GET** | `/api/dashboard/summary` | Dashboard | Dashboard Summary | No | 200, 422 |
| **GET** | `/api/discounts` | Discounts | All Discounts | No | 200, 422 |
| **POST** | `/api/discounts` | Discounts | Add Global Discount | Yes | 200, 422 |
| **GET** | `/api/discounts/` | Discounts | All Discounts | No | 200, 422 |
| **POST** | `/api/discounts/` | Discounts | Add Global Discount | Yes | 200, 422 |
| **PUT** | `/api/discounts/{discount_id}` | Discounts | Edit Global Discount Route | Yes | 200, 422 |
| **PATCH** | `/api/discounts/{discount_id}/amend` | Discounts | Amend Global Discount Route | Yes | 200, 422 |
| **PATCH** | `/api/discounts/{discount_id}/deactivate` | Discounts | Deactivate Global Discount Route | Yes | 200, 422 |
| **GET** | `/api/discounts/{discount_id}/history` | Discounts | Global Discount History | No | 200, 422 |
| **GET** | `/api/discounts/{discount_id}/usage` | Discounts | Global Discount Usage | No | 200, 422 |
| **GET** | `/api/email-logs` | Email Logs | List Email Logs | No | 200, 422 |
| **GET** | `/api/email-logs/` | Email Logs | List Email Logs | No | 200, 422 |
| **GET** | `/api/email-logs/deliveries` | Email Logs | List Email Deliveries | No | 200, 422 |
| **POST** | `/api/email-logs/deliveries/{delivery_id}/retry` | Email Logs | Retry Email Delivery | No | 200, 422 |
| **GET** | `/api/email-templates/` | Email Templates | List Templates | No | 200, 422 |
| **POST** | `/api/email-templates/` | Email Templates | Add Template | Yes | 200, 422 |
| **DELETE** | `/api/email-templates/{template_id}` | Email Templates | Remove Template | No | 200, 422 |
| **GET** | `/api/email-templates/{template_id}` | Email Templates | Detail Template | No | 200, 422 |
| **PUT** | `/api/email-templates/{template_id}` | Email Templates | Edit Template | Yes | 200, 422 |
| **GET** | `/api/email-templates/{template_id}/preview` | Email Templates | Preview | No | 200, 422 |
| **POST** | `/api/email-templates/{template_id}/test` | Email Templates | Send Test | Yes | 200, 422 |
| **GET** | `/api/geo/cities` | Geo Reference | Geo Cities | No | 200, 422 |
| **GET** | `/api/geo/countries` | Geo Reference | Geo Countries | No | 200 |
| **GET** | `/api/geo/states` | Geo Reference | Geo States | No | 200, 422 |
| **GET** | `/api/health` | Other | Health | No | 200 |
| **GET** | `/api/integrations/external-tours/viator/clicks/summary` | External Tours (Admin) | Viator Click Summary | No | 200, 422 |
| **GET** | `/api/integrations/external-tours/viator/mappings` | External Tours (Admin) | Viator Mappings | No | 200, 422 |
| **PUT** | `/api/integrations/external-tours/viator/mappings/{mapping_id}` | External Tours (Admin) | Viator Update Mapping | Yes | 200, 422 |
| **PUT** | `/api/integrations/external-tours/viator/settings` | External Tours (Admin) | Viator Update Settings | Yes | 200, 422 |
| **GET** | `/api/integrations/external-tours/viator/status` | External Tours (Admin) | Viator Status | No | 200 |
| **POST** | `/api/integrations/external-tours/viator/sync-destinations` | External Tours (Admin) | Viator Sync Destinations | No | 200 |
| **POST** | `/api/integrations/external-tours/viator/test-connection` | External Tours (Admin) | Viator Test Connection | No | 200 |
| **GET** | `/api/invoices` | Invoices | Invoices | No | 200, 422 |
| **GET** | `/api/invoices/` | Invoices | Invoices | No | 200, 422 |
| **POST** | `/api/invoices/generate` | Invoices | Generate | Yes | 200, 422 |
| **GET** | `/api/invoices/sample-pdf` | Invoices | Sample Pdf | No | 200, 422 |
| **GET** | `/api/invoices/{invoice_id}` | Invoices | Detail | No | 200, 422 |
| **GET** | `/api/invoices/{invoice_id}/download` | Invoices | Download | No | 200, 422 |
| **POST** | `/api/invoices/{invoice_id}/email` | Invoices | Email Invoice | Yes | 200, 422 |
| **POST** | `/api/invoices/{invoice_id}/generate-pdf` | Invoices | Generate Pdf | No | 200, 422 |
| **DELETE** | `/api/messages/booking/{message_id}` | Messaging | Delete Own Booking Message | No | 200, 422 |
| **POST** | `/api/messages/mail-reply` | Messaging | Mail Reply | Yes | 200, 422 |
| **POST** | `/api/messages/ws-ticket` | Messaging | Issue Ws Ticket | No | 200 |
| **DELETE** | `/api/messages/{message_id}` | Messaging | Delete Own Message | No | 200, 422 |
| **GET** | `/api/modules` | Admin Modules | List Admin Modules | No | 200 |
| **GET** | `/api/modules/` | Admin Modules | List Admin Modules | No | 200 |
| **GET** | `/api/modules/all` | Admin Modules | List All Modules | No | 200 |
| **PATCH** | `/api/modules/{module_id}` | Admin Modules | Update Module Status | Yes | 200, 422 |
| **GET** | `/api/notifications` | Notifications | Notifications | No | 200, 422 |
| **POST** | `/api/notifications` | Notifications | Create | Yes | 200, 422 |
| **GET** | `/api/notifications/` | Notifications | Notifications | No | 200, 422 |
| **PATCH** | `/api/notifications/mark-all-read` | Notifications | Mark All Read Route | No | 200, 422 |
| **POST** | `/api/notifications/push/broadcast` | Notifications | Push Broadcast | Yes | 200, 422 |
| **GET** | `/api/notifications/push/public-key` | Notifications | Push Public Key | No | 200 |
| **DELETE** | `/api/notifications/push/subscribe` | Notifications | Push Unsubscribe | Yes | 200, 422 |
| **POST** | `/api/notifications/push/subscribe` | Notifications | Push Subscribe | Yes | 200, 422 |
| **PATCH** | `/api/notifications/{notification_id}/read` | Notifications | Read | No | 200, 422 |
| **POST** | `/api/notifications/{notification_id}/retry` | Notifications | Retry | No | 200, 422 |
| **GET** | `/api/payments` | Payments | List Payments | No | 200, 422 |
| **GET** | `/api/payments/` | Payments | List Payments | No | 200, 422 |
| **POST** | `/api/payments/` | Payments | Add Payment | Yes | 200, 422 |
| **POST** | `/api/payments/abandon-pending` | Payment Gateways | Abandon Pending Gateway Payment | Yes | 200, 422 |
| **POST** | `/api/payments/authorize` | Payments | Authorize | Yes | 200, 422 |
| **GET** | `/api/payments/customer/{customer_id}` | Payments | Customer Payment List | No | 200, 422 |
| **GET** | `/api/payments/gateways/status` | Payment Gateways | Gateways Status | No | 200 |
| **POST** | `/api/payments/paypal/capture` | Payment Gateways | Paypal Capture | Yes | 200, 422 |
| **POST** | `/api/payments/paypal/create-order` | Payment Gateways | Paypal Create Order | Yes | 200, 422 |
| **POST** | `/api/payments/paypal/webhook` | Payment Gateways | Paypal Webhook | No | 200 |
| **POST** | `/api/payments/stripe/confirm-return` | Payment Gateways | Stripe Confirm Return | Yes | 200, 422 |
| **POST** | `/api/payments/stripe/create-session` | Payment Gateways | Stripe Create Session | Yes | 200, 422 |
| **POST** | `/api/payments/stripe/webhook` | Payment Gateways | Stripe Webhook | No | 200, 422 |
| **POST** | `/api/payments/test/simulate` | Payment Gateways | Test Simulate Payment | Yes | 200, 422 |
| **GET** | `/api/payments/{payment_id}` | Payments | Payment Detail | No | 200, 422 |
| **PUT** | `/api/payments/{payment_id}` | Payments | Edit Payment | Yes | 200, 422 |
| **POST** | `/api/payments/{payment_id}/capture` | Payments | Capture | Yes | 200, 422 |
| **POST** | `/api/payments/{payment_id}/refund` | Payments | Refund Payment | Yes | 200, 422 |
| **PATCH** | `/api/payments/{payment_id}/status` | Payments | Change Payment Status | Yes | 200, 422 |
| **POST** | `/api/payments/{payment_id}/void` | Payments | Void | Yes | 200, 422 |
| **GET** | `/api/permissions/` | Permissions | List Permissions | No | 200, 422 |
| **POST** | `/api/permissions/` | Permissions | Add Permission | Yes | 200, 422 |
| **DELETE** | `/api/permissions/{permission_id}` | Permissions | Remove Permission | No | 200, 422 |
| **GET** | `/api/permissions/{permission_id}` | Permissions | Detail Permission | No | 200, 422 |
| **PUT** | `/api/permissions/{permission_id}` | Permissions | Edit Permission | Yes | 200, 422 |
| **GET** | `/api/portal/reviews` | Reviews | Portal Reviews | No | 200 |
| **GET** | `/api/private-documents/affiliate/{doc_id}` | Private Documents | Get Affiliate Document | No | 200, 422 |
| **GET** | `/api/private-documents/agent/{doc_id}` | Private Documents | Get Agent Document | No | 200, 422 |
| **GET** | `/api/private-documents/supplier/{doc_id}` | Private Documents | Get Supplier Document | No | 200, 422 |
| **GET** | `/api/private-documents/vehicle/{vehicle_id}/photo/{index}` | Private Documents | Get Vehicle Photo | No | 200, 422 |
| **GET** | `/api/private-documents/vehicle/{vehicle_id}/{field}` | Private Documents | Get Vehicle Document | No | 200, 422 |
| **GET** | `/api/profile/me` | Profile | My Profile | No | 200 |
| **PUT** | `/api/profile/me` | Profile | Update Profile | Yes | 200, 422 |
| **PUT** | `/api/profile/password` | Profile | Update Password | Yes | 200, 422 |
| **GET** | `/api/public-leads/contact-enquiries` | Public Leads | List Contact Enquiries | No | 200, 422 |
| **GET** | `/api/public-leads/newsletter-subscribers` | Public Leads | List Newsletter Subscribers | No | 200, 422 |
| **GET** | `/api/public/categories` | Public | Public Categories | No | 200, 422 |
| **GET** | `/api/public/cities` | Public | Public Cities | No | 200, 422 |
| **POST** | `/api/public/contact` | Public | Submit Contact Message | Yes | 200, 422 |
| **GET** | `/api/public/countries` | Public | Public Countries | No | 200 |
| **GET** | `/api/public/country-pages` | Public | Public Country Pages | No | 200 |
| **GET** | `/api/public/country-pages/{slug}` | Public | Public Country Page By Slug | No | 200, 422 |
| **GET** | `/api/public/destination-guides` | Public | Public Destination Guides | No | 200 |
| **GET** | `/api/public/destination-guides/{slug}` | Public | Public Destination Guide | No | 200, 422 |
| **GET** | `/api/public/external-day-trips` | Public | Public External Day Trips | No | 200 |
| **GET** | `/api/public/external-tours/categories` | External Tours | External Categories | No | 200 |
| **POST** | `/api/public/external-tours/click` | External Tours | External Click | Yes | 200, 422 |
| **GET** | `/api/public/external-tours/config` | External Tours | External Tours Config | No | 200 |
| **GET** | `/api/public/external-tours/destinations` | External Tours | External Destinations | No | 200, 422 |
| **GET** | `/api/public/external-tours/destinations/{slug}` | External Tours | External Destination | No | 200, 422 |
| **POST** | `/api/public/external-tours/redirect` | External Tours | External Redirect | Yes | 200, 422 |
| **POST** | `/api/public/external-tours/search` | External Tours | External Search | Yes | 200, 422 |
| **POST** | `/api/public/newsletter/subscribe` | Public | Subscribe Newsletter | Yes | 200, 422 |
| **GET** | `/api/public/subcategories` | Public | Public Subcategories | No | 200, 422 |
| **GET** | `/api/public/tours` | Public | Public Tours | No | 200, 422 |
| **GET** | `/api/public/tours/featured` | Public | Featured Tours | No | 200, 422 |
| **GET** | `/api/public/tours/{country_slug}/{tour_slug}` | Public | Public Tour Detail By Slug | No | 200, 422 |
| **GET** | `/api/public/tours/{tour_id}` | Public | Public Tour Detail | No | 200, 422 |
| **GET** | `/api/public/tours/{tour_id}/brochure` | Public | Public Tour Brochure Download | No | 200, 422 |
| **GET** | `/api/public/tours/{tour_id}/deposit-options` | Public | Public Tour Deposit Options | No | 200, 422 |
| **GET** | `/api/public/tours/{tour_id}/itinerary` | Public | Public Tour Itinerary | No | 200, 422 |
| **POST** | `/api/public/tours/{tour_id}/price-quote` | Public | Public Tour Price Quote | Yes | 200, 422 |
| **GET** | `/api/public/tours/{tour_id}/review-summary` | Reviews | Public Tour Review Summary | No | 200, 422 |
| **GET** | `/api/public/tours/{tour_id}/reviews` | Reviews | Public Tour Reviews | No | 200, 422 |
| **GET** | `/api/public/viator/redirect-url` | Public | Public Viator Redirect Url | No | 200 |
| **GET** | `/api/refund-rules` | Cancellations | List Rules | No | 200, 422 |
| **POST** | `/api/refund-rules` | Cancellations | Create Rule | Yes | 200, 422 |
| **DELETE** | `/api/refund-rules/{rule_id}` | Cancellations | Delete Rule | No | 200, 422 |
| **PUT** | `/api/refund-rules/{rule_id}` | Cancellations | Update Rule | Yes | 200, 422 |
| **GET** | `/api/reports/agents` | Reports | Agent Report | No | 200, 422 |
| **GET** | `/api/reports/audience` | Reports | Audience Report | No | 200, 422 |
| **GET** | `/api/reports/audience-detail` | Reports | Audience Report Detail | No | 200, 422 |
| **GET** | `/api/reports/audience-export` | Reports | Audience Report Export | No | 200, 422 |
| **GET** | `/api/reports/audience-options` | Reports | Audience Options | No | 200, 422 |
| **GET** | `/api/reports/booking-report` | Reports | Booking Detail Report | No | 200, 422 |
| **GET** | `/api/reports/bookings` | Reports | Booking Report | No | 200, 422 |
| **GET** | `/api/reports/cancellation-refund-report` | Reports | Cancellation Refund Report | No | 200, 422 |
| **GET** | `/api/reports/cancellations` | Reports | Cancellations | No | 200, 422 |
| **GET** | `/api/reports/country-wise` | Reports | Country Wise | No | 200, 422 |
| **GET** | `/api/reports/customers` | Reports | Customer Report | No | 200, 422 |
| **GET** | `/api/reports/exports` | Reports | Exports | No | 200, 422 |
| **GET** | `/api/reports/my-bookings` | Reports | My Bookings Report | No | 200, 422 |
| **GET** | `/api/reports/my-bookings-summary` | Reports | My Bookings Summary | No | 200, 422 |
| **GET** | `/api/reports/my-earnings` | Reports | My Earnings Report | No | 200 |
| **GET** | `/api/reports/my-travellers` | Reports | My Travellers Report | No | 200 |
| **GET** | `/api/reports/overdue-payments` | Reports | Overdue Payments | No | 200 |
| **GET** | `/api/reports/payment-report` | Reports | Payment Detail Report | No | 200, 422 |
| **GET** | `/api/reports/payments` | Reports | Payment Report | No | 200, 422 |
| **GET** | `/api/reports/pending-payments` | Reports | Pending Payments | No | 200 |
| **GET** | `/api/reports/sales-revenue-report` | Reports | Sales Revenue Report | No | 200, 422 |
| **GET** | `/api/reports/schedule` | Reports | List Report Schedules | No | 200 |
| **POST** | `/api/reports/schedule` | Reports | Create Report Schedule | Yes | 200, 422 |
| **DELETE** | `/api/reports/schedule/{schedule_id}` | Reports | Delete Report Schedule | No | 200, 422 |
| **GET** | `/api/reports/snapshot` | Reports | Snapshot | No | 200 |
| **GET** | `/api/reports/summary` | Reports | Summary | No | 200, 422 |
| **GET** | `/api/reports/supplier-payout-report` | Reports | Supplier Payout Report | No | 200, 422 |
| **GET** | `/api/reports/supplier-report` | Reports | Supplier Detail Report | No | 200, 422 |
| **GET** | `/api/reports/suppliers` | Reports | Supplier Report | No | 200, 422 |
| **GET** | `/api/reports/tour-performance-report` | Reports | Tour Performance Report | No | 200, 422 |
| **GET** | `/api/roles/` | Roles | List Roles | No | 200, 422 |
| **POST** | `/api/roles/` | Roles | Add Role | Yes | 200, 422 |
| **GET** | `/api/roles/public/options` | Roles | Public Role Options | No | 200 |
| **DELETE** | `/api/roles/{role_id}` | Roles | Remove Role | No | 200, 422 |
| **GET** | `/api/roles/{role_id}` | Roles | Detail Role | No | 200, 422 |
| **PUT** | `/api/roles/{role_id}` | Roles | Edit Role | Yes | 200, 422 |
| **GET** | `/api/roles/{role_id}/permissions` | Roles | Role Permissions | No | 200, 422 |
| **POST** | `/api/roles/{role_id}/permissions` | Roles | Assign Permissions | Yes | 200, 422 |
| **GET** | `/api/sessions` | Sessions | Sessions | No | 200, 422 |
| **GET** | `/api/sessions/` | Sessions | Sessions | No | 200, 422 |
| **POST** | `/api/sessions/expire-inactive` | Sessions | Expire Inactive | No | 200, 422 |
| **GET** | `/api/sessions/login-history` | Sessions | Login History | No | 200, 422 |
| **POST** | `/api/sessions/users/{user_id}/force-logout` | Sessions | Force Logout | No | 200, 422 |
| **POST** | `/api/sessions/{session_id}/revoke` | Sessions | Revoke | No | 200, 422 |
| **GET** | `/api/settings/` | Settings | List Settings | No | 200 |
| **PUT** | `/api/settings/` | Settings | Save Settings | Yes | 200, 422 |
| **GET** | `/api/settings/api` | Settings | List Api Settings | No | 200 |
| **PUT** | `/api/settings/api` | Settings | Save Api Settings | Yes | 200, 422 |
| **GET** | `/api/settings/api/summary` | Settings | Api Settings Summary | No | 200 |
| **PUT** | `/api/settings/api/{api_name}` | Settings | Save Api Setting | Yes | 200, 422 |
| **GET** | `/api/settings/cities` | Settings | Settings Cities | No | 200, 422 |
| **GET** | `/api/settings/countries` | Settings | Settings Countries | No | 200, 422 |
| **GET** | `/api/settings/payment` | Settings | List Payment Settings | No | 200 |
| **PUT** | `/api/settings/payment` | Settings | Save Payment Settings | Yes | 200, 422 |
| **GET** | `/api/settings/payment/summary` | Settings | Payment Settings Summary | No | 200 |
| **PUT** | `/api/settings/payment/{provider_name}` | Settings | Save Payment Setting | Yes | 200, 422 |
| **POST** | `/api/settings/payment/{provider_name}/test-connection` | Settings | Test Payment Provider Connection | No | 200, 422 |
| **GET** | `/api/settings/pricing/commission-preview` | Settings | Commission Preview | No | 200, 422 |
| **GET** | `/api/settings/public` | Settings | Public Settings | No | 200 |
| **GET** | `/api/settings/security-status` | Settings | Security Status | No | 200 |
| **GET** | `/api/settings/setup-progress` | Settings | Setup Progress | No | 200 |
| **GET** | `/api/settings/smtp` | Settings | Smtp Settings Summary | No | 200 |
| **PUT** | `/api/settings/smtp` | Settings | Save Smtp Settings | Yes | 200, 422 |
| **POST** | `/api/settings/smtp/test` | Settings | Test Smtp Settings | Yes | 200, 422 |
| **GET** | `/api/settings/system` | Settings | System Settings | No | 200 |
| **PUT** | `/api/settings/system` | Settings | Save System Settings | Yes | 200, 422 |
| **GET** | `/api/states` | CMS | States | No | 200, 422 |
| **POST** | `/api/states` | CMS | Add State | Yes | 200, 422 |
| **GET** | `/api/states/{state_id}` | CMS | State Detail | No | 200, 422 |
| **PUT** | `/api/states/{state_id}` | CMS | Edit State | Yes | 200, 422 |
| **PATCH** | `/api/states/{state_id}/status` | CMS | State Status | Yes | 200, 422 |
| **GET** | `/api/supplier-ledgers` | Supplier Ledger | List Ledgers | No | 200, 422 |
| **GET** | `/api/supplier-payouts` | Supplier Ledger | List Payouts | No | 200, 422 |
| **POST** | `/api/supplier-payouts` | Supplier Ledger | Create Payout | Yes | 200, 422 |
| **POST** | `/api/supplier-payouts/{payout_id}/approve` | Supplier Ledger | Approve Payout | No | 200, 422 |
| **PATCH** | `/api/supplier-payouts/{payout_id}/mark-paid` | Supplier Ledger | Mark Paid | Yes | 200, 422 |
| **POST** | `/api/supplier-payouts/{payout_id}/mark-paid` | Supplier Ledger | Mark Paid Post | No | 200, 422 |
| **GET** | `/api/supplier-statements/{supplier_id}` | Supplier Ledger | Supplier Statement | No | 200, 422 |
| **GET** | `/api/supplier/booking-messages` | Supplier Booking Messaging | Supplier Booking Conversations | No | 200, 422 |
| **GET** | `/api/supplier/booking-messages/` | Supplier Booking Messaging | Supplier Booking Conversations | No | 200, 422 |
| **GET** | `/api/supplier/booking-messages/booking/{booking_id}` | Supplier Booking Messaging | Supplier Booking Conversation For Booking | No | 200, 422 |
| **GET** | `/api/supplier/booking-messages/unread-count` | Supplier Booking Messaging | Supplier Booking Unread | No | 200 |
| **GET** | `/api/supplier/booking-messages/{conversation_id}` | Supplier Booking Messaging | Supplier Booking Conversation Thread | No | 200, 422 |
| **POST** | `/api/supplier/booking-messages/{conversation_id}/messages` | Supplier Booking Messaging | Supplier Booking Conversation Reply | Yes | 200, 422 |
| **GET** | `/api/supplier/bookings` | Supplier Bookings | Supplier Bookings | No | 200, 422 |
| **GET** | `/api/supplier/bookings/` | Supplier Bookings | Supplier Bookings | No | 200, 422 |
| **POST** | `/api/supplier/bookings/communications/{communication_id}/replies` | Supplier Bookings | Supplier Reply Communication | Yes | 200, 422 |
| **GET** | `/api/supplier/bookings/{booking_id}` | Supplier Bookings | Supplier Booking Detail | No | 200, 422 |
| **POST** | `/api/supplier/bookings/{booking_id}/accept` | Supplier Bookings | Supplier Accept | Yes | 200, 422 |
| **PATCH** | `/api/supplier/bookings/{booking_id}/cancel` | Supplier Bookings | Supplier Cancel | Yes | 200, 422 |
| **POST** | `/api/supplier/bookings/{booking_id}/communications` | Supplier Bookings | Supplier Create Communication | Yes | 200, 422 |
| **PATCH** | `/api/supplier/bookings/{booking_id}/complete` | Supplier Bookings | Supplier Complete | Yes | 200, 422 |
| **POST** | `/api/supplier/bookings/{booking_id}/decline` | Supplier Bookings | Supplier Decline | Yes | 200, 422 |
| **PATCH** | `/api/supplier/bookings/{booking_id}/due-date` | Supplier Bookings | Supplier Set Due Date Endpoint | Yes | 200, 422 |
| **POST** | `/api/supplier/bookings/{booking_id}/notify` | Supplier Bookings | Supplier Notify | Yes | 200, 422 |
| **PATCH** | `/api/supplier/bookings/{booking_id}/ongoing` | Supplier Bookings | Supplier Start | Yes | 200, 422 |
| **GET** | `/api/supplier/bookings/{booking_id}/status-history` | Supplier Bookings | Supplier Booking History | No | 200, 422 |
| **GET** | `/api/supplier/invoices` | Supplier Invoices | Supplier Invoices | No | 200, 422 |
| **GET** | `/api/supplier/invoices/` | Supplier Invoices | Supplier Invoices | No | 200, 422 |
| **GET** | `/api/supplier/invoices/{invoice_id}/download` | Supplier Invoices | Download Supplier Invoice | No | 200, 422 |
| **GET** | `/api/supplier/messages` | Supplier Portal | Supplier Messages | No | 200 |
| **POST** | `/api/supplier/messages` | Supplier Portal | Send Supplier Message | Yes | 200, 422 |
| **GET** | `/api/suppliers` | Suppliers | Suppliers | No | 200, 422 |
| **POST** | `/api/suppliers` | Suppliers | Add Supplier | Yes | 200, 422 |
| **GET** | `/api/suppliers/` | Suppliers | Suppliers | No | 200, 422 |
| **POST** | `/api/suppliers/` | Suppliers | Add Supplier | Yes | 200, 422 |
| **POST** | `/api/suppliers/bulk-approve` | Suppliers | Bulk Approve | Yes | 200, 422 |
| **POST** | `/api/suppliers/bulk-reject` | Suppliers | Bulk Reject | Yes | 200, 422 |
| **GET** | `/api/suppliers/document-requirements` | Suppliers | Supplier Document Requirements | No | 200 |
| **GET** | `/api/suppliers/export` | Suppliers | Export Suppliers Endpoint | No | 200 |
| **GET** | `/api/suppliers/me` | Suppliers | My Supplier | No | 200 |
| **PATCH** | `/api/suppliers/me` | Suppliers | Edit My Supplier | Yes | 200, 422 |
| **PUT** | `/api/suppliers/me` | Suppliers | Edit My Supplier | Yes | 200, 422 |
| **POST** | `/api/suppliers/me/accept-commission` | Suppliers | Accept My Commission | No | 200 |
| **POST** | `/api/suppliers/me/bank-details/edit-request` | Suppliers | Request My Bank Detail Edit | No | 200 |
| **GET** | `/api/suppliers/me/commission-calculator` | Suppliers | My Commission Calculator | No | 200, 422 |
| **POST** | `/api/suppliers/me/onboarding/complete` | Suppliers | Complete My Onboarding | No | 200 |
| **GET** | `/api/suppliers/me/vehicles` | Suppliers | Get My Vehicles | No | 200 |
| **POST** | `/api/suppliers/me/vehicles` | Suppliers | Add My Vehicle | Yes | 200, 422 |
| **DELETE** | `/api/suppliers/me/vehicles/{vehicle_id}` | Suppliers | Delete My Vehicle | No | 200, 422 |
| **PATCH** | `/api/suppliers/me/vehicles/{vehicle_id}` | Suppliers | Update My Vehicle | Yes | 200, 422 |
| **PUT** | `/api/suppliers/me/vehicles/{vehicle_id}` | Suppliers | Update My Vehicle | Yes | 200, 422 |
| **DELETE** | `/api/suppliers/me/vehicles/{vehicle_id}/photos` | Suppliers | Delete Vehicle Photo | No | 200, 422 |
| **POST** | `/api/suppliers/me/vehicles/{vehicle_id}/photos` | Suppliers | Upload Vehicle Photos | Yes | 200, 422 |
| **POST** | `/api/suppliers/me/vehicles/{vehicle_id}/upload/{field}` | Suppliers | Upload Vehicle File | Yes | 200, 422 |
| **GET** | `/api/suppliers/pending` | Suppliers | Pending Suppliers | No | 200, 422 |
| **POST** | `/api/suppliers/register` | Suppliers | Register Supplier | Yes | 200, 422 |
| **POST** | `/api/suppliers/submit-verification` | Suppliers | Submit Verification | No | 200 |
| **POST** | `/api/suppliers/verify-email` | Suppliers | Verify Supplier Email | Yes | 200, 422 |
| **GET** | `/api/suppliers/{supplier_id}` | Suppliers | Supplier Detail | No | 200, 422 |
| **PATCH** | `/api/suppliers/{supplier_id}` | Suppliers | Edit Supplier | Yes | 200, 422 |
| **PUT** | `/api/suppliers/{supplier_id}` | Suppliers | Edit Supplier | Yes | 200, 422 |
| **POST** | `/api/suppliers/{supplier_id}/accept` | Suppliers | Approve | No | 200, 422 |
| **PATCH** | `/api/suppliers/{supplier_id}/approve` | Suppliers | Approve | No | 200, 422 |
| **POST** | `/api/suppliers/{supplier_id}/approve` | Suppliers | Approve | No | 200, 422 |
| **POST** | `/api/suppliers/{supplier_id}/bank-details/reject` | Suppliers | Reject Bank Detail Edit | Yes | 200, 422 |
| **POST** | `/api/suppliers/{supplier_id}/bank-details/unlock` | Suppliers | Unlock Bank Detail Edit | No | 200, 422 |
| **POST** | `/api/suppliers/{supplier_id}/deactivate` | Suppliers | Deactivate Supplier | Yes | 200, 422 |
| **GET** | `/api/suppliers/{supplier_id}/documents` | Suppliers | Get Supplier Documents | No | 200, 422 |
| **POST** | `/api/suppliers/{supplier_id}/documents` | Suppliers | Upload Supplier Document | Yes | 200, 422 |
| **PATCH** | `/api/suppliers/{supplier_id}/documents/{document_id}/review` | Suppliers | Review Document | Yes | 200, 422 |
| **GET** | `/api/suppliers/{supplier_id}/ledger` | Supplier Ledger | Supplier Ledger | No | 200, 422 |
| **PATCH** | `/api/suppliers/{supplier_id}/partial-approve` | Suppliers | Partial Approve | Yes | 200, 422 |
| **POST** | `/api/suppliers/{supplier_id}/partial-approve` | Suppliers | Partial Approve | Yes | 200, 422 |
| **POST** | `/api/suppliers/{supplier_id}/reactivate` | Suppliers | Reactivate Supplier | Yes | 200, 422 |
| **PATCH** | `/api/suppliers/{supplier_id}/reject` | Suppliers | Reject | Yes | 200, 422 |
| **POST** | `/api/suppliers/{supplier_id}/reject` | Suppliers | Reject | Yes | 200, 422 |
| **POST** | `/api/suppliers/{supplier_id}/request-information` | Suppliers | Partial Approve | Yes | 200, 422 |
| **POST** | `/api/suppliers/{supplier_id}/request-reupload` | Suppliers | Request Reupload | Yes | 200, 422 |
| **POST** | `/api/suppliers/{supplier_id}/submit-verification` | Suppliers | Submit Verification By Id | No | 200, 422 |
| **POST** | `/api/suppliers/{supplier_id}/suspend` | Suppliers | Suspend Supplier | Yes | 200, 422 |
| **PATCH** | `/api/suppliers/{supplier_id}/vehicles/{vehicle_id}/review` | Suppliers | Review Vehicle | Yes | 200, 422 |
| **GET** | `/api/tour-categories` | CMS | Categories | No | 200, 422 |
| **POST** | `/api/tour-categories` | CMS | Add Category | Yes | 200, 422 |
| **GET** | `/api/tour-categories/{category_id}` | CMS | Category Detail | No | 200, 422 |
| **PUT** | `/api/tour-categories/{category_id}` | CMS | Edit Category | Yes | 200, 422 |
| **PATCH** | `/api/tour-categories/{category_id}/status` | CMS | Category Status | Yes | 200, 422 |
| **GET** | `/api/tour-subcategories` | CMS | Subcategories | No | 200, 422 |
| **POST** | `/api/tour-subcategories` | CMS | Add Subcategory | Yes | 200, 422 |
| **GET** | `/api/tour-subcategories/{subcategory_id}` | CMS | Subcategory Detail | No | 200, 422 |
| **PUT** | `/api/tour-subcategories/{subcategory_id}` | CMS | Edit Subcategory | Yes | 200, 422 |
| **PATCH** | `/api/tour-subcategories/{subcategory_id}/status` | CMS | Subcategory Status | Yes | 200, 422 |
| **GET** | `/api/tours` | CMS | Tours | No | 200, 422 |
| **POST** | `/api/tours` | CMS | Add Tour | Yes | 200, 422 |
| **GET** | `/api/tours/categories` | Tour Detail | Tour Categories | No | 200, 422 |
| **POST** | `/api/tours/import` | CMS | Tours Import | Yes | 200, 422 |
| **GET** | `/api/tours/import-template` | CMS | Tours Import Template | No | 200 |
| **GET** | `/api/tours/pending-approval` | Tour Versions | List Pending | No | 200, 422 |
| **DELETE** | `/api/tours/{tour_id}` | CMS | Remove Tour | No | 200, 422 |
| **GET** | `/api/tours/{tour_id}` | CMS | Tour Detail | No | 200, 422 |
| **PUT** | `/api/tours/{tour_id}` | CMS | Edit Tour | Yes | 200, 422 |
| **GET** | `/api/tours/{tour_id}/accommodation-extras` | Tour Detail | Tour Accommodations | No | 200, 422 |
| **POST** | `/api/tours/{tour_id}/accommodation-extras` | Tour Detail | Add Accommodation | Yes | 200, 422 |
| **DELETE** | `/api/tours/{tour_id}/accommodation-extras/{extra_id}` | Tour Detail | Remove Accommodation | No | 200, 422 |
| **PUT** | `/api/tours/{tour_id}/accommodation-extras/{extra_id}` | Tour Detail | Edit Accommodation | Yes | 200, 422 |
| **GET** | `/api/tours/{tour_id}/availability` | Tour Detail | Tour Availability | No | 200, 422 |
| **PUT** | `/api/tours/{tour_id}/availability` | Tour Detail | Save Availability | Yes | 200, 422 |
| **POST** | `/api/tours/{tour_id}/calculate-price` | Tour Detail | Tour Calculate Price | Yes | 200, 422 |
| **GET** | `/api/tours/{tour_id}/calendar` | Tour Detail | Tour Calendar | No | 200, 422 |
| **POST** | `/api/tours/{tour_id}/calendar` | Tour Detail | Add Calendar | Yes | 200, 422 |
| **DELETE** | `/api/tours/{tour_id}/calendar/{calendar_id}` | Tour Detail | Remove Calendar | No | 200, 422 |
| **PUT** | `/api/tours/{tour_id}/calendar/{calendar_id}` | Tour Detail | Edit Calendar | Yes | 200, 422 |
| **PATCH** | `/api/tours/{tour_id}/commission` | CMS | Tour Commission | Yes | 200, 422 |
| **GET** | `/api/tours/{tour_id}/date-prices` | Tour Detail | Tour Date Prices | No | 200, 422 |
| **POST** | `/api/tours/{tour_id}/date-prices` | Tour Detail | Add Date Price | Yes | 200, 422 |
| **DELETE** | `/api/tours/{tour_id}/date-prices/{date_price_id}` | Tour Detail | Remove Date Price | No | 200, 422 |
| **PUT** | `/api/tours/{tour_id}/date-prices/{date_price_id}` | Tour Detail | Edit Date Price | Yes | 200, 422 |
| **GET** | `/api/tours/{tour_id}/discounts` | Tour Detail | Tour Discounts | No | 200, 422 |
| **POST** | `/api/tours/{tour_id}/discounts` | Tour Detail | Add Discount | Yes | 200, 422 |
| **PUT** | `/api/tours/{tour_id}/discounts/{discount_id}` | Tour Detail | Edit Tour Discount | Yes | 200, 422 |
| **PATCH** | `/api/tours/{tour_id}/discounts/{discount_id}/amend` | Tour Detail | Amend Tour Discount | Yes | 200, 422 |
| **PATCH** | `/api/tours/{tour_id}/discounts/{discount_id}/deactivate` | Tour Detail | Deactivate Tour Discount | Yes | 200, 422 |
| **GET** | `/api/tours/{tour_id}/discounts/{discount_id}/history` | Tour Detail | Tour Discount History | No | 200, 422 |
| **GET** | `/api/tours/{tour_id}/exclusions` | Tour Detail | Tour Exclusions | No | 200, 422 |
| **POST** | `/api/tours/{tour_id}/exclusions` | Tour Detail | Add Exclusion | Yes | 200, 422 |
| **DELETE** | `/api/tours/{tour_id}/exclusions/{exclusion_id}` | Tour Detail | Remove Exclusion | No | 200, 422 |
| **PUT** | `/api/tours/{tour_id}/exclusions/{exclusion_id}` | Tour Detail | Edit Exclusion | Yes | 200, 422 |
| **GET** | `/api/tours/{tour_id}/export` | CMS | Tour Export | No | 200, 422 |
| **GET** | `/api/tours/{tour_id}/extensions` | Tour Detail | Tour Extensions | No | 200, 422 |
| **POST** | `/api/tours/{tour_id}/extensions` | Tour Detail | Add Extension | Yes | 200, 422 |
| **DELETE** | `/api/tours/{tour_id}/extensions/{extension_id}` | Tour Detail | Remove Extension | No | 200, 422 |
| **PUT** | `/api/tours/{tour_id}/extensions/{extension_id}` | Tour Detail | Edit Extension | Yes | 200, 422 |
| **GET** | `/api/tours/{tour_id}/gallery` | Tour Detail | Tour Gallery | No | 200, 422 |
| **POST** | `/api/tours/{tour_id}/gallery` | Tour Detail | Add Gallery Image | Yes | 200, 422 |
| **DELETE** | `/api/tours/{tour_id}/gallery/{image_id}` | Tour Detail | Remove Gallery Image | No | 200, 422 |
| **PUT** | `/api/tours/{tour_id}/gallery/{image_id}` | Tour Detail | Edit Gallery Image | Yes | 200, 422 |
| **GET** | `/api/tours/{tour_id}/group-discount-tiers` | Tour Detail | Tour Group Discount Tiers | No | 200, 422 |
| **POST** | `/api/tours/{tour_id}/group-discount-tiers` | Tour Detail | Add Group Discount Tier | Yes | 200, 422 |
| **DELETE** | `/api/tours/{tour_id}/group-discount-tiers/{tier_id}` | Tour Detail | Remove Group Discount Tier | No | 200, 422 |
| **PUT** | `/api/tours/{tour_id}/group-discount-tiers/{tier_id}` | Tour Detail | Edit Group Discount Tier | Yes | 200, 422 |
| **PATCH** | `/api/tours/{tour_id}/group-size` | Tour Detail | Update Tour Group Size | Yes | 200, 422 |
| **GET** | `/api/tours/{tour_id}/highlights` | Tour Detail | Tour Highlights | No | 200, 422 |
| **POST** | `/api/tours/{tour_id}/highlights` | Tour Detail | Add Highlight | Yes | 200, 422 |
| **DELETE** | `/api/tours/{tour_id}/highlights/{highlight_id}` | Tour Detail | Remove Highlight | No | 200, 422 |
| **PUT** | `/api/tours/{tour_id}/highlights/{highlight_id}` | Tour Detail | Edit Highlight | Yes | 200, 422 |
| **GET** | `/api/tours/{tour_id}/inclusions` | Tour Detail | Tour Inclusions | No | 200, 422 |
| **POST** | `/api/tours/{tour_id}/inclusions` | Tour Detail | Add Inclusion | Yes | 200, 422 |
| **DELETE** | `/api/tours/{tour_id}/inclusions/{inclusion_id}` | Tour Detail | Remove Inclusion | No | 200, 422 |
| **PUT** | `/api/tours/{tour_id}/inclusions/{inclusion_id}` | Tour Detail | Edit Inclusion | Yes | 200, 422 |
| **GET** | `/api/tours/{tour_id}/itineraries` | Tour Detail | Tour Itineraries | No | 200, 422 |
| **POST** | `/api/tours/{tour_id}/itineraries` | Tour Detail | Add Itinerary | Yes | 200, 422 |
| **PATCH** | `/api/tours/{tour_id}/itineraries/reorder` | Tour Detail | Reorder Tour Itineraries | Yes | 200, 422 |
| **DELETE** | `/api/tours/{tour_id}/itineraries/{itinerary_id}` | Tour Detail | Remove Itinerary | No | 200, 422 |
| **GET** | `/api/tours/{tour_id}/itineraries/{itinerary_id}` | Tour Detail | Get Itinerary | No | 200, 422 |
| **PUT** | `/api/tours/{tour_id}/itineraries/{itinerary_id}` | Tour Detail | Edit Itinerary | Yes | 200, 422 |
| **GET** | `/api/tours/{tour_id}/markup` | Tour Detail | Get Tour Markup | No | 200, 422 |
| **PUT** | `/api/tours/{tour_id}/markup` | Tour Detail | Update Tour Markup | Yes | 200, 422 |
| **GET** | `/api/tours/{tour_id}/optional-activities` | Tour Detail | Tour Activities | No | 200, 422 |
| **POST** | `/api/tours/{tour_id}/optional-activities` | Tour Detail | Add Activity | Yes | 200, 422 |
| **DELETE** | `/api/tours/{tour_id}/optional-activities/{activity_id}` | Tour Detail | Remove Activity | No | 200, 422 |
| **PUT** | `/api/tours/{tour_id}/optional-activities/{activity_id}` | Tour Detail | Edit Activity | Yes | 200, 422 |
| **GET** | `/api/tours/{tour_id}/overview` | Tour Detail | Tour Overview | No | 200, 422 |
| **POST** | `/api/tours/{tour_id}/overview` | Tour Detail | Save Tour Overview | Yes | 200, 422 |
| **PUT** | `/api/tours/{tour_id}/overview` | Tour Detail | Update Tour Overview | Yes | 200, 422 |
| **GET** | `/api/tours/{tour_id}/pricing` | Tour Detail | Tour Pricing | No | 200, 422 |
| **POST** | `/api/tours/{tour_id}/pricing` | Tour Detail | Add Pricing | Yes | 200, 422 |
| **DELETE** | `/api/tours/{tour_id}/pricing/{pricing_id}` | Tour Detail | Remove Pricing | No | 200, 422 |
| **PUT** | `/api/tours/{tour_id}/pricing/{pricing_id}` | Tour Detail | Edit Pricing | Yes | 200, 422 |
| **GET** | `/api/tours/{tour_id}/review-comments` | Tour Versions | List Review Comments | No | 200, 422 |
| **POST** | `/api/tours/{tour_id}/review-comments` | Tour Versions | Create Review Comment | Yes | 200, 422 |
| **PATCH** | `/api/tours/{tour_id}/review-comments/{comment_id}/resolve` | Tour Versions | Resolve Review Comment | No | 200, 422 |
| **GET** | `/api/tours/{tour_id}/similar-tours` | Tour Detail | Tour Similar | No | 200, 422 |
| **POST** | `/api/tours/{tour_id}/similar-tours` | Tour Detail | Add Tour Similar | Yes | 200, 422 |
| **DELETE** | `/api/tours/{tour_id}/similar-tours/{similar_id}` | Tour Detail | Remove Similar | No | 200, 422 |
| **PATCH** | `/api/tours/{tour_id}/status` | CMS | Tour Status | Yes | 200, 422 |
| **POST** | `/api/tours/{tour_id}/submit-for-approval` | Tour Versions | Submit For Approval | No | 200, 422 |
| **GET** | `/api/tours/{tour_id}/unavailable-dates` | Tour Detail | Tour Unavailable | No | 200, 422 |
| **POST** | `/api/tours/{tour_id}/unavailable-dates` | Tour Detail | Add Unavailable | Yes | 200, 422 |
| **DELETE** | `/api/tours/{tour_id}/unavailable-dates/{date_id}` | Tour Detail | Remove Unavailable | No | 200, 422 |
| **GET** | `/api/tours/{tour_id}/versions` | Tour Versions | List Versions | No | 200, 422 |
| **PATCH** | `/api/tours/{tour_id}/versions/{version_id}/approve` | Tour Versions | Approve Version | No | 200, 422 |
| **PATCH** | `/api/tours/{tour_id}/versions/{version_id}/reject` | Tour Versions | Reject Version | Yes | 200, 422 |
| **POST** | `/api/tours/{tour_id}/withdraw` | Tour Versions | Withdraw Submission | No | 200, 422 |
| **POST** | `/api/uploads/admin-asset` | Uploads | Upload Admin Asset | Yes | 200, 422 |
| **POST** | `/api/uploads/profile-image` | Uploads | Upload Profile Image | Yes | 200, 422 |
| **GET** | `/api/users/` | Users | List Users | No | 200, 422 |
| **POST** | `/api/users/` | Users | Add User | Yes | 200, 422 |
| **DELETE** | `/api/users/{user_id}` | Users | Remove User | No | 200, 422 |
| **GET** | `/api/users/{user_id}` | Users | User Detail | No | 200, 422 |
| **PUT** | `/api/users/{user_id}` | Users | Edit User | Yes | 200, 422 |
| **POST** | `/api/users/{user_id}/activate` | Users | Activate User Account | Yes | 200, 422 |
| **POST** | `/api/users/{user_id}/deactivate` | Users | Deactivate User Account | Yes | 200, 422 |
| **POST** | `/api/users/{user_id}/reactivate` | Users | Reactivate User Account | No | 200, 422 |
| **POST** | `/api/users/{user_id}/roles` | Users | Assign User Roles | Yes | 200, 422 |
| **POST** | `/api/users/{user_id}/send-reset-mail` | Users | Send Reset Mail | No | 200, 422 |
| **GET** | `/api/wishlist` | Wishlist | User Wishlist | No | 200 |
| **DELETE** | `/api/wishlist/{tour_id}` | Wishlist | Delete User Wishlist Item | No | 200, 422 |
| **POST** | `/api/wishlist/{tour_id}` | Wishlist | Add User Wishlist Item | No | 200, 422 |
| **GET** | `/r/{code}` | Affiliate Redirect | Redirect Affiliate Link | No | 200, 422 |

## Endpoints Grouped by Functional Module

### Activity Logs (6 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/activity-logs/` | Activity Logs | entity_type, action, actor_user_id, page, limit, search |
| **GET** | `/api/activity-logs` | Activity Logs | entity_type, action, actor_user_id, page, limit, search |
| **GET** | `/api/activity-logs/export` | Export Logs | - |
| **GET** | `/api/audit-logs` | Activity Logs | entity_type, action, actor_user_id, page, limit, search |
| **GET** | `/api/audit-logs/` | Activity Logs | entity_type, action, actor_user_id, page, limit, search |
| **GET** | `/api/audit-logs/export` | Export Logs | - |

### Admin Messaging (6 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/admin/messages/conversations` | Conversations | type, page, limit |
| **GET** | `/api/admin/messages/unread-summary` | Unread Summary | - |
| **GET** | `/api/admin/messages/booking-conversations/{booking_id}` | Booking Conversations For Admin | booking_id |
| **POST** | `/api/admin/messages/booking-conversations/{conversation_id}/messages` | Booking Conversation Reply As Admin | conversation_id |
| **GET** | `/api/admin/messages/conversations/{conversation_id}` | Conversation Thread | conversation_id |
| **POST** | `/api/admin/messages/conversations/{conversation_id}/messages` | Reply | conversation_id |

### Admin Modules (4 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/modules/` | List Admin Modules | - |
| **GET** | `/api/modules` | List Admin Modules | - |
| **GET** | `/api/modules/all` | List All Modules | - |
| **PATCH** | `/api/modules/{module_id}` | Update Module Status | module_id |

### Affiliate Commission Rules (7 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/affiliate-commission-rules/` | List Rules | affiliate_id, tour_id, is_active, page, limit, search |
| **POST** | `/api/affiliate-commission-rules/` | Create Rule | - |
| **GET** | `/api/affiliate-commission-rules` | List Rules | affiliate_id, tour_id, is_active, page, limit, search |
| **POST** | `/api/affiliate-commission-rules` | Create Rule | - |
| **GET** | `/api/affiliate-commission-rules/{rule_id}` | Rule Detail | rule_id |
| **PUT** | `/api/affiliate-commission-rules/{rule_id}` | Update Rule | rule_id |
| **DELETE** | `/api/affiliate-commission-rules/{rule_id}` | Delete Rule | rule_id |

### Affiliate Links (Admin) (10 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/affiliate-links/` | List Links | affiliate_id, tour_id, status, page, limit, search |
| **POST** | `/api/affiliate-links/` | Create Link | - |
| **GET** | `/api/affiliate-links` | List Links | affiliate_id, tour_id, status, page, limit, search |
| **POST** | `/api/affiliate-links` | Create Link | - |
| **GET** | `/api/affiliate-links/{link_id}` | Link Detail | link_id |
| **PUT** | `/api/affiliate-links/{link_id}` | Update Link | link_id |
| **DELETE** | `/api/affiliate-links/{link_id}` | Delete Link | link_id |
| **POST** | `/api/affiliate-links/{link_id}/activate` | Activate Link | link_id |
| **POST** | `/api/affiliate-links/{link_id}/disable` | Disable Link | link_id |
| **POST** | `/api/affiliate-links/{link_id}/duplicate` | Duplicate Link | link_id, campaign_name |

### Affiliate Payouts (12 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/affiliate/payout-methods` | List Payout Methods | - |
| **POST** | `/api/affiliate/payout-methods` | Create Payout Method | - |
| **PUT** | `/api/affiliate/payout-methods/{method_id}` | Update Payout Method | method_id |
| **DELETE** | `/api/affiliate/payout-methods/{method_id}` | Delete Payout Method | method_id |
| **GET** | `/api/affiliate/wallet` | Wallet Summary | - |
| **GET** | `/api/affiliate/wallet/transactions` | Wallet Transactions | page, limit, search |
| **POST** | `/api/affiliate/payout-requests` | Request Payout | - |
| **GET** | `/api/admin/affiliate-payouts` | Admin List Payouts | status, page, limit, search |
| **POST** | `/api/affiliate-payouts/{payout_id}/approve` | Approve Payout | payout_id |
| **POST** | `/api/affiliate-payouts/{payout_id}/reject` | Reject Payout | payout_id |
| **POST** | `/api/affiliate-payouts/{payout_id}/processing` | Mark Processing | payout_id |
| **POST** | `/api/affiliate-payouts/{payout_id}/mark-paid` | Mark Paid | payout_id |

### Affiliate Redirect (1 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/r/{code}` | Redirect Affiliate Link | code |

### Affiliate Tracking (12 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/affiliates/{affiliate_id}/links` | List Links | affiliate_id |
| **POST** | `/api/affiliates/{affiliate_id}/links` | Create Link | affiliate_id |
| **GET** | `/api/affiliates/{affiliate_id}/links/{link_id}` | Link Detail | affiliate_id, link_id |
| **PUT** | `/api/affiliates/{affiliate_id}/links/{link_id}` | Update Own Link | affiliate_id, link_id |
| **GET** | `/api/affiliates/track/{ref_code}` | Track Click | ref_code |
| **GET** | `/api/affiliates/{affiliate_id}/clicks` | List Clicks | affiliate_id, page, limit, search |
| **GET** | `/api/affiliates/{affiliate_id}/conversions` | List Conversions | affiliate_id, page, limit, search |
| **GET** | `/api/affiliates/{affiliate_id}/commissions` | Get Commissions | affiliate_id |
| **GET** | `/api/affiliate-payouts` | List Payouts | affiliate_id, page, limit, search |
| **POST** | `/api/affiliate-payouts` | Create Payout | - |
| **GET** | `/api/affiliate/messages` | Affiliate Messages | - |
| **POST** | `/api/affiliate/messages` | Send Affiliate Message | - |

### Affiliates (24 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/affiliates/me` | My Affiliate | - |
| **PUT** | `/api/affiliates/me` | Edit My Affiliate | - |
| **PATCH** | `/api/affiliates/me` | Edit My Affiliate | - |
| **POST** | `/api/affiliates/me/accept-commission` | Accept My Commission | - |
| **POST** | `/api/affiliates/me/bank-details/edit-request` | Request My Bank Detail Edit | - |
| **GET** | `/api/affiliates/document-requirements` | Affiliate Document Requirements | - |
| **POST** | `/api/affiliates/submit-verification` | Submit My Verification | - |
| **GET** | `/api/affiliates/` | Affiliates | country_id, status, approval_status, start_date, end_date, sort_by, page, limit, search |
| **POST** | `/api/affiliates/` | Add Affiliate | - |
| **GET** | `/api/affiliates` | Affiliates | country_id, status, approval_status, start_date, end_date, sort_by, page, limit, search |
| **POST** | `/api/affiliates` | Add Affiliate | - |
| **GET** | `/api/affiliates/{affiliate_id}` | Affiliate Detail | affiliate_id |
| **PUT** | `/api/affiliates/{affiliate_id}` | Edit Affiliate | affiliate_id |
| **GET** | `/api/affiliates/{affiliate_id}/commission-calculator` | Affiliate Commission Calculator | affiliate_id, amount, tour_id |
| **GET** | `/api/affiliates/{affiliate_id}/documents` | Get Affiliate Documents | affiliate_id |
| **POST** | `/api/affiliates/{affiliate_id}/documents` | Upload Affiliate Document | affiliate_id |
| **PATCH** | `/api/affiliates/{affiliate_id}/documents/{document_id}/review` | Review Document | affiliate_id, document_id |
| **PATCH** | `/api/affiliates/{affiliate_id}/approve` | Approve | affiliate_id |
| **POST** | `/api/affiliates/{affiliate_id}/bank-details/unlock` | Unlock Bank Detail Edit | affiliate_id |
| **POST** | `/api/affiliates/{affiliate_id}/bank-details/reject` | Reject Bank Detail Edit | affiliate_id |
| **PATCH** | `/api/affiliates/{affiliate_id}/reject` | Reject | affiliate_id |
| **POST** | `/api/affiliates/{affiliate_id}/activate` | Activate | affiliate_id |
| **POST** | `/api/affiliates/{affiliate_id}/suspend` | Suspend | affiliate_id |
| **PATCH** | `/api/affiliates/{affiliate_id}/api-link` | Api Link | affiliate_id |

### Agent Ledger (9 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/agent-ledgers` | List Ledgers | agent_id, status, page, limit, search |
| **GET** | `/api/agents/{agent_id}/ledger` | Agent Ledger | agent_id, status, page, limit, search |
| **GET** | `/api/agent-statements/{agent_id}` | Agent Statement | agent_id |
| **GET** | `/api/agent-payouts` | List Payouts | agent_id, status, page, limit, search |
| **POST** | `/api/agent-payouts` | Create Payout | - |
| **POST** | `/api/agent-payouts/{payout_id}/approve` | Approve Payout | payout_id |
| **POST** | `/api/agent-payouts/{payout_id}/reject` | Reject Payout | payout_id |
| **POST** | `/api/agent-payouts/{payout_id}/mark-paid` | Mark Paid Post | payout_id |
| **PATCH** | `/api/agent-payouts/{payout_id}/mark-paid` | Mark Paid | payout_id |

### Agent Portal (2 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/agent/messages` | Agent Messages | - |
| **POST** | `/api/agent/messages` | Send Agent Message | - |

### Agents (37 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **POST** | `/api/agents/register` | Register Agent | - |
| **POST** | `/api/agents/verify-email` | Verify Agent Email | - |
| **POST** | `/api/agents/submit-verification` | Submit Verification | - |
| **GET** | `/api/agents/pending` | Pending Agents | page, limit, search |
| **GET** | `/api/agents/export` | Export Agents Endpoint | - |
| **GET** | `/api/agents/` | Agents | country_id, status, approval_status, start_date, end_date, sort_by, page, limit, search |
| **POST** | `/api/agents/` | Add Agent | - |
| **GET** | `/api/agents` | Agents | country_id, status, approval_status, start_date, end_date, sort_by, page, limit, search |
| **POST** | `/api/agents` | Add Agent | - |
| **GET** | `/api/agents/me` | My Agent | - |
| **PUT** | `/api/agents/me` | Edit My Agent | - |
| **PATCH** | `/api/agents/me` | Edit My Agent | - |
| **GET** | `/api/agents/document-requirements` | Document Requirements | - |
| **POST** | `/api/agents/me/bank-details/edit-request` | Request My Bank Detail Edit | - |
| **POST** | `/api/agents/me/commission-request` | Request My Commission | - |
| **POST** | `/api/agents/me/accept-commission` | Accept My Commission | - |
| **GET** | `/api/agents/me/commission-calculator` | My Commission Calculator | amount |
| **GET** | `/api/agents/{agent_id}` | Agent Detail | agent_id |
| **PUT** | `/api/agents/{agent_id}` | Edit Agent | agent_id |
| **PATCH** | `/api/agents/{agent_id}` | Edit Agent | agent_id |
| **GET** | `/api/agents/{agent_id}/documents` | Get Agent Documents | agent_id |
| **POST** | `/api/agents/{agent_id}/documents` | Upload Agent Document | agent_id |
| **PATCH** | `/api/agents/{agent_id}/documents/{document_id}/review` | Review Document | agent_id, document_id |
| **POST** | `/api/agents/bulk-approve` | Bulk Approve | - |
| **POST** | `/api/agents/bulk-reject` | Bulk Reject | - |
| **POST** | `/api/agents/{agent_id}/approve` | Approve | agent_id |
| **PATCH** | `/api/agents/{agent_id}/approve` | Approve | agent_id |
| **POST** | `/api/agents/{agent_id}/bank-details/unlock` | Unlock Bank Detail Edit | agent_id |
| **POST** | `/api/agents/{agent_id}/bank-details/reject` | Reject Bank Detail Edit | agent_id |
| **POST** | `/api/agents/{agent_id}/reject` | Reject | agent_id |
| **PATCH** | `/api/agents/{agent_id}/reject` | Reject | agent_id |
| **POST** | `/api/agents/{agent_id}/partial-approve` | Partial Approve | agent_id |
| **PATCH** | `/api/agents/{agent_id}/partial-approve` | Partial Approve | agent_id |
| **POST** | `/api/agents/{agent_id}/request-correction` | Request Correction | agent_id |
| **POST** | `/api/agents/{agent_id}/discount` | Discount | agent_id |
| **PATCH** | `/api/agents/{agent_id}/discount` | Discount | agent_id |
| **POST** | `/api/agents/{agent_id}/commission-request/reject` | Reject Commission Request | agent_id |

### Authentication (29 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **POST** | `/api/auth/register` | Register | - |
| **POST** | `/api/auth/register/customer` | Register Customer | - |
| **POST** | `/api/auth/register/supplier` | Register Supplier | - |
| **POST** | `/api/auth/register/agent` | Register Agent | - |
| **POST** | `/api/auth/login` | Login | - |
| **POST** | `/api/auth/2fa/login-verify` | Two Factor Login Verify | - |
| **POST** | `/api/auth/2fa/setup` | Two Factor Setup | - |
| **POST** | `/api/auth/2fa/enable` | Two Factor Enable | - |
| **POST** | `/api/auth/2fa/disable` | Two Factor Disable | - |
| **POST** | `/api/auth/otp/request` | Otp Request | - |
| **POST** | `/api/auth/otp/verify` | Otp Verify | - |
| **GET** | `/api/auth/account-status` | Account Status | - |
| **GET** | `/api/auth/me` | Current Session | - |
| **POST** | `/api/auth/forgot-password` | Forgot Password Request | - |
| **POST** | `/api/auth/reset-password` | Reset Password Request | - |
| **GET** | `/api/auth/reset-password/validate` | Validate Reset Password Link | token |
| **POST** | `/api/auth/refresh-token` | Refresh Token | - |
| **POST** | `/api/auth/refresh` | Refresh | - |
| **POST** | `/api/auth/logout` | Logout | - |
| **POST** | `/api/auth/logout-all` | Logout All | - |
| **GET** | `/api/auth/verify-email` | Verify Email Link | token |
| **POST** | `/api/auth/verify-email` | Verify Email Request | - |
| **GET** | `/api/auth/verify-email/validate` | Validate Verification Link | token |
| **POST** | `/api/auth/complete-registration` | Complete Registration Request | - |
| **POST** | `/api/auth/create-password` | Create Registration Password | - |
| **POST** | `/api/auth/resend-verification` | Resend Verification | - |
| **POST** | `/api/auth/change-registration-email` | Change Email | - |
| **GET** | `/api/auth/login-history` | Login History | limit |
| **POST** | `/api/auth/force-logout` | Force Logout | - |

### Booking Calendar (3 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **POST** | `/api/bookings/{booking_id}/calendar-sync` | Sync Calendar | booking_id |
| **GET** | `/api/bookings/{booking_id}/calendar-event` | Get Calendar Event | booking_id |
| **GET** | `/api/bookings/{booking_id}/calendar-event/download` | Download Ics | booking_id |

### Booking Messaging (2 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/bookings/{booking_id}/conversation` | Booking Conversation Thread | booking_id |
| **POST** | `/api/bookings/{booking_id}/conversation/messages` | Send Booking Conversation Message | booking_id |

### Bookings (23 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/bookings/` | List Bookings | customer_id, booking_status, payment_status, supplier_acceptance_status, cancellation_source, country_id, supplier_id, agent_id, tour_id, start_date, end_date, sort_by, page, limit, search |
| **POST** | `/api/bookings/` | Add Booking | - |
| **GET** | `/api/bookings` | List Bookings | customer_id, booking_status, payment_status, supplier_acceptance_status, cancellation_source, country_id, supplier_id, agent_id, tour_id, start_date, end_date, sort_by, page, limit, search |
| **POST** | `/api/bookings` | Add Booking | - |
| **GET** | `/api/bookings/export` | Export Bookings Endpoint | - |
| **GET** | `/api/bookings/upcoming` | Upcoming Bookings | - |
| **POST** | `/api/bookings/expire-stale` | Expire Stale Bookings Endpoint | older_than_minutes |
| **POST** | `/api/bookings/calculate-price` | Calculate Price | - |
| **GET** | `/api/bookings/{booking_id}` | Booking Detail | booking_id |
| **PUT** | `/api/bookings/{booking_id}` | Edit Booking | booking_id |
| **POST** | `/api/bookings/{booking_id}/hide-from-agent` | Hide From Agent Bookings | booking_id |
| **GET** | `/api/bookings/{booking_id}/modifications` | Booking Modifications | booking_id |
| **POST** | `/api/bookings/{booking_id}/modifications` | Request Booking Modification | booking_id |
| **POST** | `/api/bookings/{booking_id}/modifications/{modification_id}/approve` | Approve Booking Modification | booking_id, modification_id |
| **POST** | `/api/bookings/{booking_id}/modifications/{modification_id}/reject` | Reject Booking Modification | booking_id, modification_id |
| **PATCH** | `/api/bookings/{booking_id}/travel-date` | Change Booking Travel Date | booking_id |
| **PATCH** | `/api/bookings/{booking_id}/status` | Change Booking Status | booking_id |
| **GET** | `/api/bookings/{booking_id}/payment-link` | Booking Payment Link | booking_id |
| **GET** | `/api/bookings/{booking_id}/status-history` | Booking Status History | booking_id |
| **POST** | `/api/bookings/{booking_id}/assign-supplier` | Assign Supplier Endpoint | booking_id |
| **PATCH** | `/api/bookings/{booking_id}/cancel` | Cancel Booking Endpoint | booking_id |
| **POST** | `/api/bookings/{booking_id}/communications` | Create Booking Communication | booking_id |
| **POST** | `/api/bookings/communications/{communication_id}/replies` | Reply Booking Communication | communication_id |

### CMS (41 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/countries` | Countries | page, limit, search |
| **POST** | `/api/countries` | Add Country | - |
| **PATCH** | `/api/countries/bulk-disable` | Bulk Disable Countries | search |
| **GET** | `/api/countries/{country_id}` | Country Detail | country_id |
| **PUT** | `/api/countries/{country_id}` | Edit Country | country_id |
| **PATCH** | `/api/countries/{country_id}/status` | Country Status | country_id |
| **GET** | `/api/currencies` | Currencies | page, limit, search |
| **POST** | `/api/currencies` | Add Currency | - |
| **GET** | `/api/currencies/{currency_id}` | Currency Detail | currency_id |
| **PUT** | `/api/currencies/{currency_id}` | Edit Currency | currency_id |
| **PATCH** | `/api/currencies/{currency_id}/status` | Currency Status | currency_id |
| **GET** | `/api/states` | States | country_id, page, limit, search |
| **POST** | `/api/states` | Add State | - |
| **GET** | `/api/states/{state_id}` | State Detail | state_id |
| **PUT** | `/api/states/{state_id}` | Edit State | state_id |
| **PATCH** | `/api/states/{state_id}/status` | State Status | state_id |
| **GET** | `/api/cities` | Cities | country_id, state_id, page, limit, search |
| **POST** | `/api/cities` | Add City | - |
| **GET** | `/api/cities/{city_id}` | City Detail | city_id |
| **PUT** | `/api/cities/{city_id}` | Edit City | city_id |
| **PATCH** | `/api/cities/{city_id}/status` | City Status | city_id |
| **GET** | `/api/tour-categories` | Categories | page, limit, search |
| **POST** | `/api/tour-categories` | Add Category | - |
| **GET** | `/api/tour-categories/{category_id}` | Category Detail | category_id |
| **PUT** | `/api/tour-categories/{category_id}` | Edit Category | category_id |
| **PATCH** | `/api/tour-categories/{category_id}/status` | Category Status | category_id |
| **GET** | `/api/tour-subcategories` | Subcategories | category_id, page, limit, search |
| **POST** | `/api/tour-subcategories` | Add Subcategory | - |
| **GET** | `/api/tour-subcategories/{subcategory_id}` | Subcategory Detail | subcategory_id |
| **PUT** | `/api/tour-subcategories/{subcategory_id}` | Edit Subcategory | subcategory_id |
| **PATCH** | `/api/tour-subcategories/{subcategory_id}/status` | Subcategory Status | subcategory_id |
| **GET** | `/api/tours` | Tours | country_id, city_id, category_id, status, supplier_id, page, limit, search |
| **POST** | `/api/tours` | Add Tour | - |
| **GET** | `/api/tours/import-template` | Tours Import Template | - |
| **POST** | `/api/tours/import` | Tours Import | - |
| **GET** | `/api/tours/{tour_id}` | Tour Detail | tour_id |
| **PUT** | `/api/tours/{tour_id}` | Edit Tour | tour_id |
| **DELETE** | `/api/tours/{tour_id}` | Remove Tour | tour_id |
| **GET** | `/api/tours/{tour_id}/export` | Tour Export | tour_id |
| **PATCH** | `/api/tours/{tour_id}/status` | Tour Status | tour_id |
| **PATCH** | `/api/tours/{tour_id}/commission` | Tour Commission | tour_id |

### Cancellations (11 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **POST** | `/api/bookings/{booking_id}/cancel-request` | Customer Cancel Request | booking_id |
| **GET** | `/api/cancellations` | List Cancellations | status, customer_id, page, limit, search |
| **PATCH** | `/api/cancellations/{request_id}/approve` | Approve Cancellation | request_id |
| **PATCH** | `/api/bookings/{booking_id}/cancellation-request/approve` | Approve Booking Cancellation | booking_id |
| **PATCH** | `/api/bookings/{booking_id}/cancellation-request/reject` | Reject Booking Cancellation | booking_id |
| **PATCH** | `/api/cancellations/{request_id}/reject` | Reject Cancellation | request_id |
| **POST** | `/api/cancellations/{request_id}/process-refund` | Process Refund | request_id |
| **GET** | `/api/refund-rules` | List Rules | tour_id, supplier_id |
| **POST** | `/api/refund-rules` | Create Rule | - |
| **PUT** | `/api/refund-rules/{rule_id}` | Update Rule | rule_id |
| **DELETE** | `/api/refund-rules/{rule_id}` | Delete Rule | rule_id |

### Chatbot (12 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **POST** | `/api/chatbot/chat` | Chat | - |
| **GET** | `/api/chatbot/health` | Chatbot Health | - |
| **POST** | `/api/chatbot/feedback` | Submit Chat Feedback | - |
| **POST** | `/api/chatbot/admin/reindex` | Admin Reindex | - |
| **GET** | `/api/chatbot/faqs` | Public Faqs | - |
| **GET** | `/api/chatbot/admin/faqs` | Admin List Faqs | is_public, page, limit, search |
| **POST** | `/api/chatbot/admin/faqs` | Admin Create Faq | - |
| **PUT** | `/api/chatbot/admin/faqs/{faq_id}` | Admin Update Faq | faq_id |
| **DELETE** | `/api/chatbot/admin/faqs/{faq_id}` | Admin Delete Faq | faq_id |
| **GET** | `/api/chatbot/admin/sessions` | Admin List Sessions | page, limit, search |
| **GET** | `/api/chatbot/admin/analytics` | Admin Analytics | days |
| **GET** | `/api/chatbot/admin/sessions/{session_id}/messages` | Admin Session Messages | session_id |

### Checkout (5 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/checkout/admin/sessions` | Admin List Checkout Sessions | status, page, limit, search |
| **POST** | `/api/checkout/start` | Start Checkout | - |
| **GET** | `/api/checkout/session/{session_key}` | Get Checkout Session | session_key |
| **PATCH** | `/api/checkout/session/{session_key}` | Update Checkout Session | session_key |
| **POST** | `/api/checkout/session/{session_key}/confirm` | Confirm Checkout | session_key |

### Client (13 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/client/config` | Client Config | - |
| **GET** | `/api/client/tours` | Public Tours | page, limit, search, country_id, city_id, category_id |
| **GET** | `/api/client/tours/{tour_id}` | Public Tour Detail | tour_id |
| **GET** | `/api/client/tours/{tour_id}/overview` | Public Tour Overview | tour_id |
| **GET** | `/api/client/tours/{tour_id}/itineraries` | Public Tour Itineraries | tour_id |
| **GET** | `/api/client/tours/{tour_id}/inclusions` | Public Tour Inclusions | tour_id |
| **GET** | `/api/client/tours/{tour_id}/exclusions` | Public Tour Exclusions | tour_id |
| **GET** | `/api/client/tours/{tour_id}/highlights` | Public Tour Highlights | tour_id |
| **GET** | `/api/client/tours/{tour_id}/similar-tours` | Public Tour Similar Tours | tour_id |
| **GET** | `/api/client/tours/{tour_id}/gallery` | Public Tour Gallery | tour_id |
| **GET** | `/api/client/tours/{tour_id}/optional-activities` | Public Tour Activities | tour_id |
| **GET** | `/api/client/tours/{tour_id}/calendar` | Public Tour Calendar | tour_id |
| **GET** | `/api/client/tours/{tour_id}/pricing` | Public Tour Pricing | tour_id |

### Currency (5 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/currency/rates` | Currency Rates | base |
| **GET** | `/api/currency/admin/rates` | Admin Currency Rates | - |
| **POST** | `/api/currency/admin/refresh` | Admin Refresh Currency Rates | - |
| **GET** | `/api/currency/convert` | Currency Convert | amount, from, to |
| **GET** | `/api/currency/context` | Currency Context | country |

### Customer Portal (22 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/customer/profile` | Customer Profile | - |
| **PUT** | `/api/customer/profile` | Update Customer Profile | - |
| **POST** | `/api/customer/change-password` | Change Customer Password | - |
| **GET** | `/api/customer/bookings` | Customer Bookings | booking_status, payment_status, page, limit, search |
| **POST** | `/api/customer/bookings` | Create Customer Booking | - |
| **GET** | `/api/customer/bookings/{booking_id}` | Customer Booking Detail | booking_id |
| **GET** | `/api/customer/bookings/{booking_id}/itinerary` | Customer Booking Itinerary | booking_id |
| **GET** | `/api/customer/bookings/{booking_id}/confirmation-receipt` | Customer Booking Confirmation Receipt | booking_id |
| **POST** | `/api/customer/bookings/{booking_id}/cancel` | Request Booking Cancellation | booking_id |
| **POST** | `/api/customer/bookings/{booking_id}/remove-unpaid` | Remove Unpaid Booking | booking_id |
| **POST** | `/api/customer/bookings/{booking_id}/pay` | Record Customer Manual Payment | booking_id |
| **GET** | `/api/customer/payments` | Customer Payments | payment_status, payment_method, page, limit, search |
| **GET** | `/api/customer/invoices` | Customer Invoices | page, limit, search |
| **GET** | `/api/customer/invoices/{invoice_id}/download` | Customer Invoice Download | invoice_id |
| **GET** | `/api/customer/messages` | Customer Messages | - |
| **POST** | `/api/customer/messages` | Send Customer Portal Message | - |
| **GET** | `/api/customer/travellers` | Customer Saved Travellers | - |
| **POST** | `/api/customer/travellers` | Add Saved Traveller | - |
| **PUT** | `/api/customer/travellers/{traveller_id}` | Update Saved Traveller | traveller_id |
| **DELETE** | `/api/customer/travellers/{traveller_id}` | Delete Saved Traveller | traveller_id |
| **GET** | `/api/customer/cancellations` | Customer Cancellations | page, limit, search |
| **POST** | `/api/customer/bookings/calculate-price` | Customer Calculate Price | - |

### Customers (21 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/customers/` | List Customers | country, country_id, status, payment_status, booking_status, start_date, end_date, sort_by, sort_order, agent_id, page, limit, search |
| **POST** | `/api/customers/` | Add Customer | - |
| **GET** | `/api/customers` | List Customers | country, country_id, status, payment_status, booking_status, start_date, end_date, sort_by, sort_order, agent_id, page, limit, search |
| **POST** | `/api/customers` | Add Customer | - |
| **POST** | `/api/customers/link` | Link Existing Customer | - |
| **GET** | `/api/customers/me` | My Customer | - |
| **PUT** | `/api/customers/me` | Edit My Customer | - |
| **PATCH** | `/api/customers/me` | Edit My Customer | - |
| **GET** | `/api/customers/{customer_id}` | Customer Detail | customer_id |
| **PUT** | `/api/customers/{customer_id}` | Edit Customer | customer_id |
| **PATCH** | `/api/customers/{customer_id}/status` | Change Customer Status | customer_id |
| **POST** | `/api/customers/{customer_id}/block` | Block Customer Account Compat | customer_id |
| **PATCH** | `/api/customers/{customer_id}/block` | Block Customer Account | customer_id |
| **POST** | `/api/customers/{customer_id}/unblock` | Unblock Customer Account Compat | customer_id |
| **PATCH** | `/api/customers/{customer_id}/unblock` | Unblock Customer Account | customer_id |
| **POST** | `/api/customers/{customer_id}/reset-password` | Reset Customer Login Password | customer_id |
| **GET** | `/api/customers/{customer_id}/bookings` | Customer Booking History | customer_id, booking_status, payment_status, page, limit, search |
| **GET** | `/api/customers/{customer_id}/payments` | Customer Payment History | customer_id, payment_status, payment_method, page, limit, search |
| **GET** | `/api/customers/{customer_id}/communications` | Customer Communication History | customer_id, page, limit, search |
| **POST** | `/api/customers/{customer_id}/communications` | Send Customer Communication | customer_id |
| **POST** | `/api/customers/me/bookings` | Self Create Booking | - |

### Dashboard (8 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/dashboard/me` | My Dashboard | - |
| **GET** | `/api/dashboard/summary` | Dashboard Summary | start_date, end_date, country_id, supplier_id, agent_id, booking_id, booking_status |
| **GET** | `/api/dashboard/charts` | Dashboard Charts | start_date, end_date, country_id, booking_id, booking_status |
| **GET** | `/api/dashboard/recent-activities` | Recent Activities | start_date, end_date, country_id, booking_id, booking_status |
| **GET** | `/api/dashboard/alerts` | Dashboard Alerts | - |
| **GET** | `/api/dashboard/bookings` | Booking Analytics | start_date, end_date, country_id |
| **GET** | `/api/dashboard/revenue` | Revenue Analytics | start_date, end_date, country_id |
| **GET** | `/api/dashboard/payments` | Payment Summary | start_date, end_date, country_id |

### Discounts (9 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/discounts/` | All Discounts | scope, search |
| **POST** | `/api/discounts/` | Add Global Discount | - |
| **GET** | `/api/discounts` | All Discounts | scope, search |
| **POST** | `/api/discounts` | Add Global Discount | - |
| **PUT** | `/api/discounts/{discount_id}` | Edit Global Discount Route | discount_id |
| **PATCH** | `/api/discounts/{discount_id}/amend` | Amend Global Discount Route | discount_id |
| **PATCH** | `/api/discounts/{discount_id}/deactivate` | Deactivate Global Discount Route | discount_id |
| **GET** | `/api/discounts/{discount_id}/history` | Global Discount History | discount_id |
| **GET** | `/api/discounts/{discount_id}/usage` | Global Discount Usage | discount_id |

### Email Logs (4 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/email-logs/deliveries` | List Email Deliveries | status, stale_only, page, limit, search |
| **POST** | `/api/email-logs/deliveries/{delivery_id}/retry` | Retry Email Delivery | delivery_id |
| **GET** | `/api/email-logs/` | List Email Logs | status, entity_type, page, limit, search |
| **GET** | `/api/email-logs` | List Email Logs | status, entity_type, page, limit, search |

### Email Templates (7 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/email-templates/` | List Templates | page, limit, search |
| **POST** | `/api/email-templates/` | Add Template | - |
| **GET** | `/api/email-templates/{template_id}` | Detail Template | template_id |
| **PUT** | `/api/email-templates/{template_id}` | Edit Template | template_id |
| **DELETE** | `/api/email-templates/{template_id}` | Remove Template | template_id |
| **GET** | `/api/email-templates/{template_id}/preview` | Preview | template_id |
| **POST** | `/api/email-templates/{template_id}/test` | Send Test | template_id |

### External Tours (7 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/public/external-tours/config` | External Tours Config | - |
| **GET** | `/api/public/external-tours/destinations` | External Destinations | search, limit |
| **GET** | `/api/public/external-tours/destinations/{slug}` | External Destination | slug |
| **GET** | `/api/public/external-tours/categories` | External Categories | - |
| **POST** | `/api/public/external-tours/search` | External Search | - |
| **POST** | `/api/public/external-tours/click` | External Click | - |
| **POST** | `/api/public/external-tours/redirect` | External Redirect | - |

### External Tours (Admin) (7 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/integrations/external-tours/viator/status` | Viator Status | - |
| **POST** | `/api/integrations/external-tours/viator/test-connection` | Viator Test Connection | - |
| **POST** | `/api/integrations/external-tours/viator/sync-destinations` | Viator Sync Destinations | - |
| **PUT** | `/api/integrations/external-tours/viator/settings` | Viator Update Settings | - |
| **GET** | `/api/integrations/external-tours/viator/mappings` | Viator Mappings | search, status, type, page, limit |
| **PUT** | `/api/integrations/external-tours/viator/mappings/{mapping_id}` | Viator Update Mapping | mapping_id |
| **GET** | `/api/integrations/external-tours/viator/clicks/summary` | Viator Click Summary | days |

### Geo Reference (3 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/geo/countries` | Geo Countries | - |
| **GET** | `/api/geo/states` | Geo States | country_id |
| **GET** | `/api/geo/cities` | Geo Cities | state_id, country_id |

### Geo Seed (2 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **POST** | `/api/admin/seed/geo` | Trigger Geo Seed | countries, include_cities |
| **GET** | `/api/admin/seed/geo/status` | Geo Seed Status | - |

### Google Authentication (2 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/auth/google` | Google Login | redirect |
| **GET** | `/api/auth/google/callback` | Google Callback | code, state, error |

### Invoices (8 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/invoices/` | Invoices | booking_id, customer_id, page, limit, search |
| **GET** | `/api/invoices` | Invoices | booking_id, customer_id, page, limit, search |
| **POST** | `/api/invoices/generate` | Generate | - |
| **GET** | `/api/invoices/sample-pdf` | Sample Pdf | template_type, currency, tour_name, booking_code, recipient_business_name, recipient_contact_name, recipient_address, recipient_email, recipient_phone, tour_price, addons_total, discount_total, tax_amount, adult_count, child_count, travel_date, lead_traveller, pickup |
| **GET** | `/api/invoices/{invoice_id}` | Detail | invoice_id |
| **POST** | `/api/invoices/{invoice_id}/generate-pdf` | Generate Pdf | invoice_id |
| **GET** | `/api/invoices/{invoice_id}/download` | Download | invoice_id |
| **POST** | `/api/invoices/{invoice_id}/email` | Email Invoice | invoice_id |

### Messaging (4 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **POST** | `/api/messages/ws-ticket` | Issue Ws Ticket | - |
| **DELETE** | `/api/messages/{message_id}` | Delete Own Message | message_id |
| **DELETE** | `/api/messages/booking/{message_id}` | Delete Own Booking Message | message_id |
| **POST** | `/api/messages/mail-reply` | Mail Reply | - |

### Notifications (10 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/notifications/` | Notifications | user_id, is_read, entity_type, entity_id, notification_type, page, limit, search |
| **GET** | `/api/notifications` | Notifications | user_id, is_read, entity_type, entity_id, notification_type, page, limit, search |
| **POST** | `/api/notifications` | Create | - |
| **PATCH** | `/api/notifications/mark-all-read` | Mark All Read Route | user_id |
| **PATCH** | `/api/notifications/{notification_id}/read` | Read | notification_id |
| **POST** | `/api/notifications/{notification_id}/retry` | Retry | notification_id |
| **GET** | `/api/notifications/push/public-key` | Push Public Key | - |
| **POST** | `/api/notifications/push/subscribe` | Push Subscribe | - |
| **DELETE** | `/api/notifications/push/subscribe` | Push Unsubscribe | - |
| **POST** | `/api/notifications/push/broadcast` | Push Broadcast | - |

### Other (2 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/` | Home | - |
| **GET** | `/api/health` | Health | - |

### Payment Gateways (9 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **POST** | `/api/payments/abandon-pending` | Abandon Pending Gateway Payment | - |
| **POST** | `/api/payments/stripe/create-session` | Stripe Create Session | - |
| **POST** | `/api/payments/stripe/webhook` | Stripe Webhook | stripe-signature |
| **POST** | `/api/payments/stripe/confirm-return` | Stripe Confirm Return | - |
| **POST** | `/api/payments/paypal/create-order` | Paypal Create Order | - |
| **POST** | `/api/payments/paypal/capture` | Paypal Capture | - |
| **POST** | `/api/payments/paypal/webhook` | Paypal Webhook | - |
| **GET** | `/api/payments/gateways/status` | Gateways Status | - |
| **POST** | `/api/payments/test/simulate` | Test Simulate Payment | - |

### Payments (11 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/payments/` | List Payments | customer_id, booking_id, payment_status, payment_method, gateway, start_date, end_date, page, limit, search |
| **POST** | `/api/payments/` | Add Payment | - |
| **GET** | `/api/payments` | List Payments | customer_id, booking_id, payment_status, payment_method, gateway, start_date, end_date, page, limit, search |
| **POST** | `/api/payments/authorize` | Authorize | - |
| **GET** | `/api/payments/customer/{customer_id}` | Customer Payment List | customer_id, payment_status, payment_method, page, limit, search |
| **GET** | `/api/payments/{payment_id}` | Payment Detail | payment_id |
| **PUT** | `/api/payments/{payment_id}` | Edit Payment | payment_id |
| **PATCH** | `/api/payments/{payment_id}/status` | Change Payment Status | payment_id |
| **POST** | `/api/payments/{payment_id}/capture` | Capture | payment_id |
| **POST** | `/api/payments/{payment_id}/void` | Void | payment_id |
| **POST** | `/api/payments/{payment_id}/refund` | Refund Payment | payment_id |

### Permissions (10 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/permissions/` | List Permissions | page, limit, search |
| **POST** | `/api/permissions/` | Add Permission | - |
| **GET** | `/api/permissions/{permission_id}` | Detail Permission | permission_id |
| **PUT** | `/api/permissions/{permission_id}` | Edit Permission | permission_id |
| **DELETE** | `/api/permissions/{permission_id}` | Remove Permission | permission_id |
| **GET** | `/api/admin/permissions/` | List Permissions | page, limit, search |
| **POST** | `/api/admin/permissions/` | Add Permission | - |
| **GET** | `/api/admin/permissions/{permission_id}` | Detail Permission | permission_id |
| **PUT** | `/api/admin/permissions/{permission_id}` | Edit Permission | permission_id |
| **DELETE** | `/api/admin/permissions/{permission_id}` | Remove Permission | permission_id |

### Private Documents (5 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/private-documents/supplier/{doc_id}` | Get Supplier Document | doc_id |
| **GET** | `/api/private-documents/agent/{doc_id}` | Get Agent Document | doc_id |
| **GET** | `/api/private-documents/affiliate/{doc_id}` | Get Affiliate Document | doc_id |
| **GET** | `/api/private-documents/vehicle/{vehicle_id}/{field}` | Get Vehicle Document | vehicle_id, field |
| **GET** | `/api/private-documents/vehicle/{vehicle_id}/photo/{index}` | Get Vehicle Photo | vehicle_id, index |

### Profile (3 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/profile/me` | My Profile | - |
| **PUT** | `/api/profile/me` | Update Profile | - |
| **PUT** | `/api/profile/password` | Update Password | - |

### Public (20 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **POST** | `/api/public/contact` | Submit Contact Message | - |
| **POST** | `/api/public/newsletter/subscribe` | Subscribe Newsletter | - |
| **GET** | `/api/public/tours` | Public Tours | search, country, city, destination, min_rating, category, subcategory, min_days, max_days, min_price, max_price, departure_month, available_only, sort, page, limit |
| **GET** | `/api/public/tours/featured` | Featured Tours | limit |
| **GET** | `/api/public/tours/{tour_id}/deposit-options` | Public Tour Deposit Options | tour_id, travel_date |
| **POST** | `/api/public/tours/{tour_id}/price-quote` | Public Tour Price Quote | tour_id |
| **GET** | `/api/public/tours/{tour_id}/brochure` | Public Tour Brochure Download | tour_id, inline |
| **GET** | `/api/public/tours/{tour_id}/itinerary` | Public Tour Itinerary | tour_id, download |
| **GET** | `/api/public/tours/{country_slug}/{tour_slug}` | Public Tour Detail By Slug | country_slug, tour_slug, travel_date |
| **GET** | `/api/public/tours/{tour_id}` | Public Tour Detail | tour_id, travel_date |
| **GET** | `/api/public/categories` | Public Categories | country |
| **GET** | `/api/public/subcategories` | Public Subcategories | category |
| **GET** | `/api/public/countries` | Public Countries | - |
| **GET** | `/api/public/country-pages` | Public Country Pages | - |
| **GET** | `/api/public/country-pages/{slug}` | Public Country Page By Slug | slug |
| **GET** | `/api/public/destination-guides` | Public Destination Guides | - |
| **GET** | `/api/public/destination-guides/{slug}` | Public Destination Guide | slug |
| **GET** | `/api/public/cities` | Public Cities | country, limit |
| **GET** | `/api/public/external-day-trips` | Public External Day Trips | - |
| **GET** | `/api/public/viator/redirect-url` | Public Viator Redirect Url | - |

### Public Leads (2 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/public-leads/contact-enquiries` | List Contact Enquiries | audience, page, limit, search |
| **GET** | `/api/public-leads/newsletter-subscribers` | List Newsletter Subscribers | page, limit, search |

### Reports (30 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/reports/summary` | Summary | period, start_date, end_date |
| **GET** | `/api/reports/bookings` | Booking Report | period, start_date, end_date |
| **GET** | `/api/reports/payments` | Payment Report | period, start_date, end_date |
| **GET** | `/api/reports/pending-payments` | Pending Payments | - |
| **GET** | `/api/reports/overdue-payments` | Overdue Payments | - |
| **GET** | `/api/reports/country-wise` | Country Wise | period, start_date, end_date |
| **GET** | `/api/reports/cancellations` | Cancellations | period, start_date, end_date |
| **GET** | `/api/reports/suppliers` | Supplier Report | period, start_date, end_date |
| **GET** | `/api/reports/agents` | Agent Report | period, start_date, end_date |
| **GET** | `/api/reports/customers` | Customer Report | period, start_date, end_date |
| **GET** | `/api/reports/audience-options` | Audience Options | audience |
| **GET** | `/api/reports/audience` | Audience Report | audience, entity_id, period, start_date, end_date |
| **GET** | `/api/reports/audience-detail` | Audience Report Detail | audience, entity_id, period, start_date, end_date |
| **GET** | `/api/reports/audience-export` | Audience Report Export | audience, entity_id, period, start_date, end_date, format |
| **GET** | `/api/reports/booking-report` | Booking Detail Report | booking_status, payment_status, country_id, supplier_id, period, start_date, end_date |
| **GET** | `/api/reports/sales-revenue-report` | Sales Revenue Report | granularity, period, start_date, end_date |
| **GET** | `/api/reports/payment-report` | Payment Detail Report | payment_status, gateway, period, start_date, end_date |
| **GET** | `/api/reports/supplier-report` | Supplier Detail Report | period, start_date, end_date |
| **GET** | `/api/reports/supplier-payout-report` | Supplier Payout Report | status, supplier_id |
| **GET** | `/api/reports/tour-performance-report` | Tour Performance Report | supplier_id, category_id, country_id |
| **GET** | `/api/reports/cancellation-refund-report` | Cancellation Refund Report | supplier_id, period, start_date, end_date |
| **GET** | `/api/reports/my-bookings` | My Bookings Report | booking_status, payment_status, period, start_date, end_date |
| **GET** | `/api/reports/my-bookings-summary` | My Bookings Summary | booking_status, payment_status, period, start_date, end_date |
| **GET** | `/api/reports/my-earnings` | My Earnings Report | - |
| **GET** | `/api/reports/my-travellers` | My Travellers Report | - |
| **GET** | `/api/reports/exports` | Exports | report, format, period, start_date, end_date, booking_status, payment_status, gateway, supplier_id, granularity |
| **GET** | `/api/reports/schedule` | List Report Schedules | - |
| **POST** | `/api/reports/schedule` | Create Report Schedule | - |
| **DELETE** | `/api/reports/schedule/{schedule_id}` | Delete Report Schedule | schedule_id |
| **GET** | `/api/reports/snapshot` | Snapshot | - |

### Reviews (9 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **POST** | `/api/customer/reviews` | Submit Review | - |
| **GET** | `/api/customer/reviews/eligibility/{booking_id}` | Get Review Eligibility | booking_id |
| **PATCH** | `/api/customer/reviews/{review_id}` | Update Review | review_id |
| **GET** | `/api/public/tours/{tour_id}/reviews` | Public Tour Reviews | tour_id, page, limit, search |
| **GET** | `/api/public/tours/{tour_id}/review-summary` | Public Tour Review Summary | tour_id |
| **GET** | `/api/portal/reviews` | Portal Reviews | - |
| **GET** | `/api/admin/reviews` | List Reviews | status, page, limit, search |
| **PATCH** | `/api/admin/reviews/{review_id}/approve` | Approve Review | review_id |
| **PATCH** | `/api/admin/reviews/{review_id}/reject` | Reject Review | review_id |

### Roles (16 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/roles/public/options` | Public Role Options | - |
| **GET** | `/api/roles/` | List Roles | page, limit, search |
| **POST** | `/api/roles/` | Add Role | - |
| **GET** | `/api/roles/{role_id}` | Detail Role | role_id |
| **PUT** | `/api/roles/{role_id}` | Edit Role | role_id |
| **DELETE** | `/api/roles/{role_id}` | Remove Role | role_id |
| **GET** | `/api/roles/{role_id}/permissions` | Role Permissions | role_id |
| **POST** | `/api/roles/{role_id}/permissions` | Assign Permissions | role_id |
| **GET** | `/api/admin/roles/public/options` | Public Role Options | - |
| **GET** | `/api/admin/roles/` | List Roles | page, limit, search |
| **POST** | `/api/admin/roles/` | Add Role | - |
| **GET** | `/api/admin/roles/{role_id}` | Detail Role | role_id |
| **PUT** | `/api/admin/roles/{role_id}` | Edit Role | role_id |
| **DELETE** | `/api/admin/roles/{role_id}` | Remove Role | role_id |
| **GET** | `/api/admin/roles/{role_id}/permissions` | Role Permissions | role_id |
| **POST** | `/api/admin/roles/{role_id}/permissions` | Assign Permissions | role_id |

### Sessions (6 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/sessions/` | Sessions | user_id, status, page, limit, search |
| **GET** | `/api/sessions` | Sessions | user_id, status, page, limit, search |
| **GET** | `/api/sessions/login-history` | Login History | user_id, status, page, limit, search |
| **POST** | `/api/sessions/expire-inactive` | Expire Inactive | days |
| **POST** | `/api/sessions/{session_id}/revoke` | Revoke | session_id |
| **POST** | `/api/sessions/users/{user_id}/force-logout` | Force Logout | user_id |

### Settings (22 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/settings/countries` | Settings Countries | search, page, limit |
| **GET** | `/api/settings/cities` | Settings Cities | search, country_id, page, limit |
| **GET** | `/api/settings/public` | Public Settings | - |
| **GET** | `/api/settings/` | List Settings | - |
| **PUT** | `/api/settings/` | Save Settings | - |
| **GET** | `/api/settings/pricing/commission-preview` | Commission Preview | sample_price |
| **GET** | `/api/settings/setup-progress` | Setup Progress | - |
| **GET** | `/api/settings/security-status` | Security Status | - |
| **GET** | `/api/settings/system` | System Settings | - |
| **PUT** | `/api/settings/system` | Save System Settings | - |
| **GET** | `/api/settings/payment` | List Payment Settings | - |
| **PUT** | `/api/settings/payment` | Save Payment Settings | - |
| **GET** | `/api/settings/payment/summary` | Payment Settings Summary | - |
| **PUT** | `/api/settings/payment/{provider_name}` | Save Payment Setting | provider_name |
| **POST** | `/api/settings/payment/{provider_name}/test-connection` | Test Payment Provider Connection | provider_name |
| **GET** | `/api/settings/api` | List Api Settings | - |
| **PUT** | `/api/settings/api` | Save Api Settings | - |
| **GET** | `/api/settings/api/summary` | Api Settings Summary | - |
| **PUT** | `/api/settings/api/{api_name}` | Save Api Setting | api_name |
| **GET** | `/api/settings/smtp` | Smtp Settings Summary | - |
| **PUT** | `/api/settings/smtp` | Save Smtp Settings | - |
| **POST** | `/api/settings/smtp/test` | Test Smtp Settings | - |

### Social Authentication (2 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/auth/oauth/providers` | Provider Status | - |
| **GET** | `/api/auth/oauth/{provider}/start` | Start Social Auth | provider, redirect |

### Supplier Booking Messaging (6 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/supplier/booking-messages/` | Supplier Booking Conversations | page, limit |
| **GET** | `/api/supplier/booking-messages` | Supplier Booking Conversations | page, limit |
| **GET** | `/api/supplier/booking-messages/unread-count` | Supplier Booking Unread | - |
| **GET** | `/api/supplier/booking-messages/booking/{booking_id}` | Supplier Booking Conversation For Booking | booking_id |
| **GET** | `/api/supplier/booking-messages/{conversation_id}` | Supplier Booking Conversation Thread | conversation_id |
| **POST** | `/api/supplier/booking-messages/{conversation_id}/messages` | Supplier Booking Conversation Reply | conversation_id |

### Supplier Bookings (13 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/supplier/bookings/` | Supplier Bookings | page, limit, search |
| **GET** | `/api/supplier/bookings` | Supplier Bookings | page, limit, search |
| **GET** | `/api/supplier/bookings/{booking_id}` | Supplier Booking Detail | booking_id |
| **POST** | `/api/supplier/bookings/{booking_id}/accept` | Supplier Accept | booking_id |
| **POST** | `/api/supplier/bookings/{booking_id}/decline` | Supplier Decline | booking_id |
| **PATCH** | `/api/supplier/bookings/{booking_id}/complete` | Supplier Complete | booking_id |
| **PATCH** | `/api/supplier/bookings/{booking_id}/ongoing` | Supplier Start | booking_id |
| **PATCH** | `/api/supplier/bookings/{booking_id}/due-date` | Supplier Set Due Date Endpoint | booking_id |
| **PATCH** | `/api/supplier/bookings/{booking_id}/cancel` | Supplier Cancel | booking_id |
| **POST** | `/api/supplier/bookings/{booking_id}/communications` | Supplier Create Communication | booking_id |
| **POST** | `/api/supplier/bookings/communications/{communication_id}/replies` | Supplier Reply Communication | communication_id |
| **POST** | `/api/supplier/bookings/{booking_id}/notify` | Supplier Notify | booking_id |
| **GET** | `/api/supplier/bookings/{booking_id}/status-history` | Supplier Booking History | booking_id |

### Supplier Invoices (3 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/supplier/invoices/` | Supplier Invoices | page, limit, search |
| **GET** | `/api/supplier/invoices` | Supplier Invoices | page, limit, search |
| **GET** | `/api/supplier/invoices/{invoice_id}/download` | Download Supplier Invoice | invoice_id |

### Supplier Ledger (8 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/supplier-ledgers` | List Ledgers | supplier_id, status, page, limit, search |
| **GET** | `/api/suppliers/{supplier_id}/ledger` | Supplier Ledger | supplier_id, status, page, limit, search |
| **GET** | `/api/supplier-statements/{supplier_id}` | Supplier Statement | supplier_id |
| **GET** | `/api/supplier-payouts` | List Payouts | supplier_id, status, page, limit, search |
| **POST** | `/api/supplier-payouts` | Create Payout | - |
| **POST** | `/api/supplier-payouts/{payout_id}/approve` | Approve Payout | payout_id |
| **POST** | `/api/supplier-payouts/{payout_id}/mark-paid` | Mark Paid Post | payout_id |
| **PATCH** | `/api/supplier-payouts/{payout_id}/mark-paid` | Mark Paid | payout_id |

### Supplier Portal (2 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/supplier/messages` | Supplier Messages | - |
| **POST** | `/api/supplier/messages` | Send Supplier Message | - |

### Suppliers (49 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **POST** | `/api/suppliers/register` | Register Supplier | - |
| **POST** | `/api/suppliers/verify-email` | Verify Supplier Email | - |
| **POST** | `/api/suppliers/submit-verification` | Submit Verification | - |
| **GET** | `/api/suppliers/pending` | Pending Suppliers | page, limit, search |
| **GET** | `/api/suppliers/export` | Export Suppliers Endpoint | - |
| **GET** | `/api/suppliers/` | Suppliers | country_id, status, approval_status, start_date, end_date, sort_by, page, limit, search |
| **POST** | `/api/suppliers/` | Add Supplier | - |
| **GET** | `/api/suppliers` | Suppliers | country_id, status, approval_status, start_date, end_date, sort_by, page, limit, search |
| **POST** | `/api/suppliers` | Add Supplier | - |
| **GET** | `/api/suppliers/me` | My Supplier | - |
| **PUT** | `/api/suppliers/me` | Edit My Supplier | - |
| **PATCH** | `/api/suppliers/me` | Edit My Supplier | - |
| **GET** | `/api/suppliers/document-requirements` | Supplier Document Requirements | - |
| **POST** | `/api/suppliers/me/bank-details/edit-request` | Request My Bank Detail Edit | - |
| **GET** | `/api/suppliers/me/commission-calculator` | My Commission Calculator | adults, children, tour_id, adult_price, child_price |
| **POST** | `/api/suppliers/me/onboarding/complete` | Complete My Onboarding | - |
| **POST** | `/api/suppliers/me/accept-commission` | Accept My Commission | - |
| **GET** | `/api/suppliers/me/vehicles` | Get My Vehicles | - |
| **POST** | `/api/suppliers/me/vehicles` | Add My Vehicle | - |
| **PUT** | `/api/suppliers/me/vehicles/{vehicle_id}` | Update My Vehicle | vehicle_id |
| **PATCH** | `/api/suppliers/me/vehicles/{vehicle_id}` | Update My Vehicle | vehicle_id |
| **DELETE** | `/api/suppliers/me/vehicles/{vehicle_id}` | Delete My Vehicle | vehicle_id |
| **POST** | `/api/suppliers/me/vehicles/{vehicle_id}/upload/{field}` | Upload Vehicle File | vehicle_id, field |
| **POST** | `/api/suppliers/me/vehicles/{vehicle_id}/photos` | Upload Vehicle Photos | vehicle_id |
| **DELETE** | `/api/suppliers/me/vehicles/{vehicle_id}/photos` | Delete Vehicle Photo | vehicle_id, photo_index |
| **POST** | `/api/suppliers/{supplier_id}/submit-verification` | Submit Verification By Id | supplier_id |
| **GET** | `/api/suppliers/{supplier_id}` | Supplier Detail | supplier_id |
| **PUT** | `/api/suppliers/{supplier_id}` | Edit Supplier | supplier_id |
| **PATCH** | `/api/suppliers/{supplier_id}` | Edit Supplier | supplier_id |
| **GET** | `/api/suppliers/{supplier_id}/documents` | Get Supplier Documents | supplier_id |
| **POST** | `/api/suppliers/{supplier_id}/documents` | Upload Supplier Document | supplier_id |
| **PATCH** | `/api/suppliers/{supplier_id}/documents/{document_id}/review` | Review Document | supplier_id, document_id |
| **PATCH** | `/api/suppliers/{supplier_id}/vehicles/{vehicle_id}/review` | Review Vehicle | supplier_id, vehicle_id |
| **POST** | `/api/suppliers/bulk-approve` | Bulk Approve | - |
| **POST** | `/api/suppliers/bulk-reject` | Bulk Reject | - |
| **POST** | `/api/suppliers/{supplier_id}/accept` | Approve | supplier_id |
| **POST** | `/api/suppliers/{supplier_id}/approve` | Approve | supplier_id |
| **PATCH** | `/api/suppliers/{supplier_id}/approve` | Approve | supplier_id |
| **POST** | `/api/suppliers/{supplier_id}/bank-details/unlock` | Unlock Bank Detail Edit | supplier_id |
| **POST** | `/api/suppliers/{supplier_id}/bank-details/reject` | Reject Bank Detail Edit | supplier_id |
| **POST** | `/api/suppliers/{supplier_id}/reject` | Reject | supplier_id |
| **PATCH** | `/api/suppliers/{supplier_id}/reject` | Reject | supplier_id |
| **POST** | `/api/suppliers/{supplier_id}/request-information` | Partial Approve | supplier_id |
| **POST** | `/api/suppliers/{supplier_id}/partial-approve` | Partial Approve | supplier_id |
| **PATCH** | `/api/suppliers/{supplier_id}/partial-approve` | Partial Approve | supplier_id |
| **POST** | `/api/suppliers/{supplier_id}/request-reupload` | Request Reupload | supplier_id |
| **POST** | `/api/suppliers/{supplier_id}/deactivate` | Deactivate Supplier | supplier_id |
| **POST** | `/api/suppliers/{supplier_id}/reactivate` | Reactivate Supplier | supplier_id |
| **POST** | `/api/suppliers/{supplier_id}/suspend` | Suspend Supplier | supplier_id |

### Tour Detail (72 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/tours/categories` | Tour Categories | search, page, limit |
| **GET** | `/api/tours/{tour_id}/overview` | Tour Overview | tour_id |
| **POST** | `/api/tours/{tour_id}/overview` | Save Tour Overview | tour_id |
| **PUT** | `/api/tours/{tour_id}/overview` | Update Tour Overview | tour_id |
| **PATCH** | `/api/tours/{tour_id}/group-size` | Update Tour Group Size | tour_id |
| **GET** | `/api/tours/{tour_id}/itineraries` | Tour Itineraries | tour_id |
| **POST** | `/api/tours/{tour_id}/itineraries` | Add Itinerary | tour_id |
| **GET** | `/api/tours/{tour_id}/itineraries/{itinerary_id}` | Get Itinerary | tour_id, itinerary_id |
| **PUT** | `/api/tours/{tour_id}/itineraries/{itinerary_id}` | Edit Itinerary | tour_id, itinerary_id |
| **DELETE** | `/api/tours/{tour_id}/itineraries/{itinerary_id}` | Remove Itinerary | tour_id, itinerary_id |
| **PATCH** | `/api/tours/{tour_id}/itineraries/reorder` | Reorder Tour Itineraries | tour_id |
| **GET** | `/api/tours/{tour_id}/inclusions` | Tour Inclusions | tour_id |
| **POST** | `/api/tours/{tour_id}/inclusions` | Add Inclusion | tour_id |
| **PUT** | `/api/tours/{tour_id}/inclusions/{inclusion_id}` | Edit Inclusion | tour_id, inclusion_id |
| **DELETE** | `/api/tours/{tour_id}/inclusions/{inclusion_id}` | Remove Inclusion | tour_id, inclusion_id |
| **GET** | `/api/tours/{tour_id}/exclusions` | Tour Exclusions | tour_id |
| **POST** | `/api/tours/{tour_id}/exclusions` | Add Exclusion | tour_id |
| **PUT** | `/api/tours/{tour_id}/exclusions/{exclusion_id}` | Edit Exclusion | tour_id, exclusion_id |
| **DELETE** | `/api/tours/{tour_id}/exclusions/{exclusion_id}` | Remove Exclusion | tour_id, exclusion_id |
| **GET** | `/api/tours/{tour_id}/highlights` | Tour Highlights | tour_id |
| **POST** | `/api/tours/{tour_id}/highlights` | Add Highlight | tour_id |
| **PUT** | `/api/tours/{tour_id}/highlights/{highlight_id}` | Edit Highlight | tour_id, highlight_id |
| **DELETE** | `/api/tours/{tour_id}/highlights/{highlight_id}` | Remove Highlight | tour_id, highlight_id |
| **GET** | `/api/tours/{tour_id}/similar-tours` | Tour Similar | tour_id |
| **POST** | `/api/tours/{tour_id}/similar-tours` | Add Tour Similar | tour_id |
| **DELETE** | `/api/tours/{tour_id}/similar-tours/{similar_id}` | Remove Similar | tour_id, similar_id |
| **GET** | `/api/tours/{tour_id}/extensions` | Tour Extensions | tour_id |
| **POST** | `/api/tours/{tour_id}/extensions` | Add Extension | tour_id |
| **PUT** | `/api/tours/{tour_id}/extensions/{extension_id}` | Edit Extension | tour_id, extension_id |
| **DELETE** | `/api/tours/{tour_id}/extensions/{extension_id}` | Remove Extension | tour_id, extension_id |
| **GET** | `/api/tours/{tour_id}/gallery` | Tour Gallery | tour_id |
| **POST** | `/api/tours/{tour_id}/gallery` | Add Gallery Image | tour_id |
| **PUT** | `/api/tours/{tour_id}/gallery/{image_id}` | Edit Gallery Image | tour_id, image_id |
| **DELETE** | `/api/tours/{tour_id}/gallery/{image_id}` | Remove Gallery Image | tour_id, image_id |
| **GET** | `/api/tours/{tour_id}/markup` | Get Tour Markup | tour_id |
| **PUT** | `/api/tours/{tour_id}/markup` | Update Tour Markup | tour_id |
| **GET** | `/api/tours/{tour_id}/pricing` | Tour Pricing | tour_id |
| **POST** | `/api/tours/{tour_id}/pricing` | Add Pricing | tour_id |
| **PUT** | `/api/tours/{tour_id}/pricing/{pricing_id}` | Edit Pricing | tour_id, pricing_id |
| **DELETE** | `/api/tours/{tour_id}/pricing/{pricing_id}` | Remove Pricing | tour_id, pricing_id |
| **GET** | `/api/tours/{tour_id}/date-prices` | Tour Date Prices | tour_id |
| **POST** | `/api/tours/{tour_id}/date-prices` | Add Date Price | tour_id |
| **PUT** | `/api/tours/{tour_id}/date-prices/{date_price_id}` | Edit Date Price | tour_id, date_price_id |
| **DELETE** | `/api/tours/{tour_id}/date-prices/{date_price_id}` | Remove Date Price | tour_id, date_price_id, reason |
| **GET** | `/api/tours/{tour_id}/optional-activities` | Tour Activities | tour_id |
| **POST** | `/api/tours/{tour_id}/optional-activities` | Add Activity | tour_id |
| **PUT** | `/api/tours/{tour_id}/optional-activities/{activity_id}` | Edit Activity | tour_id, activity_id |
| **DELETE** | `/api/tours/{tour_id}/optional-activities/{activity_id}` | Remove Activity | tour_id, activity_id |
| **GET** | `/api/tours/{tour_id}/accommodation-extras` | Tour Accommodations | tour_id |
| **POST** | `/api/tours/{tour_id}/accommodation-extras` | Add Accommodation | tour_id |
| **PUT** | `/api/tours/{tour_id}/accommodation-extras/{extra_id}` | Edit Accommodation | tour_id, extra_id |
| **DELETE** | `/api/tours/{tour_id}/accommodation-extras/{extra_id}` | Remove Accommodation | tour_id, extra_id |
| **GET** | `/api/tours/{tour_id}/calendar` | Tour Calendar | tour_id |
| **POST** | `/api/tours/{tour_id}/calendar` | Add Calendar | tour_id |
| **PUT** | `/api/tours/{tour_id}/calendar/{calendar_id}` | Edit Calendar | tour_id, calendar_id |
| **DELETE** | `/api/tours/{tour_id}/calendar/{calendar_id}` | Remove Calendar | tour_id, calendar_id |
| **GET** | `/api/tours/{tour_id}/availability` | Tour Availability | tour_id |
| **PUT** | `/api/tours/{tour_id}/availability` | Save Availability | tour_id |
| **GET** | `/api/tours/{tour_id}/unavailable-dates` | Tour Unavailable | tour_id |
| **POST** | `/api/tours/{tour_id}/unavailable-dates` | Add Unavailable | tour_id |
| **DELETE** | `/api/tours/{tour_id}/unavailable-dates/{date_id}` | Remove Unavailable | tour_id, date_id |
| **GET** | `/api/tours/{tour_id}/discounts` | Tour Discounts | tour_id |
| **POST** | `/api/tours/{tour_id}/discounts` | Add Discount | tour_id |
| **PUT** | `/api/tours/{tour_id}/discounts/{discount_id}` | Edit Tour Discount | tour_id, discount_id |
| **PATCH** | `/api/tours/{tour_id}/discounts/{discount_id}/amend` | Amend Tour Discount | tour_id, discount_id |
| **PATCH** | `/api/tours/{tour_id}/discounts/{discount_id}/deactivate` | Deactivate Tour Discount | tour_id, discount_id |
| **GET** | `/api/tours/{tour_id}/discounts/{discount_id}/history` | Tour Discount History | tour_id, discount_id |
| **GET** | `/api/tours/{tour_id}/group-discount-tiers` | Tour Group Discount Tiers | tour_id |
| **POST** | `/api/tours/{tour_id}/group-discount-tiers` | Add Group Discount Tier | tour_id |
| **PUT** | `/api/tours/{tour_id}/group-discount-tiers/{tier_id}` | Edit Group Discount Tier | tour_id, tier_id |
| **DELETE** | `/api/tours/{tour_id}/group-discount-tiers/{tier_id}` | Remove Group Discount Tier | tour_id, tier_id |
| **POST** | `/api/tours/{tour_id}/calculate-price` | Tour Calculate Price | tour_id |

### Tour Versions (9 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **POST** | `/api/tours/{tour_id}/submit-for-approval` | Submit For Approval | tour_id |
| **POST** | `/api/tours/{tour_id}/withdraw` | Withdraw Submission | tour_id |
| **GET** | `/api/tours/{tour_id}/review-comments` | List Review Comments | tour_id, status |
| **POST** | `/api/tours/{tour_id}/review-comments` | Create Review Comment | tour_id |
| **PATCH** | `/api/tours/{tour_id}/review-comments/{comment_id}/resolve` | Resolve Review Comment | tour_id, comment_id |
| **GET** | `/api/tours/pending-approval` | List Pending | page, limit, search |
| **GET** | `/api/tours/{tour_id}/versions` | List Versions | tour_id, page, limit, search |
| **PATCH** | `/api/tours/{tour_id}/versions/{version_id}/approve` | Approve Version | tour_id, version_id |
| **PATCH** | `/api/tours/{tour_id}/versions/{version_id}/reject` | Reject Version | tour_id, version_id |

### Uploads (2 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **POST** | `/api/uploads/profile-image` | Upload Profile Image | - |
| **POST** | `/api/uploads/admin-asset` | Upload Admin Asset | - |

### Users (10 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/users/` | List Users | account_status, user_type, page, limit, search |
| **POST** | `/api/users/` | Add User | - |
| **GET** | `/api/users/{user_id}` | User Detail | user_id |
| **PUT** | `/api/users/{user_id}` | Edit User | user_id |
| **DELETE** | `/api/users/{user_id}` | Remove User | user_id |
| **POST** | `/api/users/{user_id}/activate` | Activate User Account | user_id |
| **POST** | `/api/users/{user_id}/deactivate` | Deactivate User Account | user_id |
| **POST** | `/api/users/{user_id}/reactivate` | Reactivate User Account | user_id |
| **POST** | `/api/users/{user_id}/send-reset-mail` | Send Reset Mail | user_id |
| **POST** | `/api/users/{user_id}/roles` | Assign User Roles | user_id |

### Website CMS (73 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/cms/homepage-banners` | List Banners | active_only, page, limit, search |
| **POST** | `/api/cms/homepage-banners` | Create Banner | - |
| **PUT** | `/api/cms/homepage-banners/{item_id}` | Update Banner | item_id |
| **DELETE** | `/api/cms/homepage-banners/{item_id}` | Delete Banner | item_id |
| **GET** | `/api/cms/popular-destinations` | List Destinations | active_only, page, limit, search |
| **POST** | `/api/cms/popular-destinations` | Create Destination | - |
| **PUT** | `/api/cms/popular-destinations/{item_id}` | Update Destination | item_id |
| **DELETE** | `/api/cms/popular-destinations/{item_id}` | Delete Destination | item_id |
| **GET** | `/api/cms/popular-tours` | List Popular Tours | active_only, published_only, page, limit, search |
| **POST** | `/api/cms/popular-tours` | Create Popular Tour | - |
| **PUT** | `/api/cms/popular-tours/{item_id}` | Update Popular Tour | item_id |
| **DELETE** | `/api/cms/popular-tours/{item_id}` | Delete Popular Tour | item_id |
| **GET** | `/api/cms/tours-on-deals` | List Deals | active_only, published_only, page, limit, search |
| **POST** | `/api/cms/tours-on-deals` | Create Deal | - |
| **PUT** | `/api/cms/tours-on-deals/{item_id}` | Update Deal | item_id |
| **DELETE** | `/api/cms/tours-on-deals/{item_id}` | Delete Deal | item_id |
| **GET** | `/api/cms/handpicked-tours` | List Handpicked Tours | active_only, published_only, page, limit, search |
| **POST** | `/api/cms/handpicked-tours` | Create Handpicked Tour | - |
| **PUT** | `/api/cms/handpicked-tours/{item_id}` | Update Handpicked Tour | item_id |
| **DELETE** | `/api/cms/handpicked-tours/{item_id}` | Delete Handpicked Tour | item_id |
| **GET** | `/api/cms/favourite-countries` | List Favourite Countries | active_only, page, limit, search |
| **POST** | `/api/cms/favourite-countries` | Create Favourite Country | - |
| **PUT** | `/api/cms/favourite-countries/{item_id}` | Update Favourite Country | item_id |
| **DELETE** | `/api/cms/favourite-countries/{item_id}` | Delete Favourite Country | item_id |
| **GET** | `/api/cms/country-pages` | List Country Pages | active_only, page, limit, search |
| **POST** | `/api/cms/country-pages` | Create Country Page | - |
| **PUT** | `/api/cms/country-pages/{item_id}` | Update Country Page | item_id |
| **DELETE** | `/api/cms/country-pages/{item_id}` | Delete Country Page | item_id |
| **GET** | `/api/cms/content-blocks/{key}` | Get Content Block | key |
| **PUT** | `/api/cms/content-blocks/{key}` | Upsert Content Block | key |
| **GET** | `/api/cms/blogs` | List Blogs | active_only, slug, search, tag, page, limit |
| **POST** | `/api/cms/blogs` | Create Blog | - |
| **GET** | `/api/cms/blogs/{item_id}` | Get Blog | item_id |
| **PUT** | `/api/cms/blogs/{item_id}` | Update Blog | item_id |
| **DELETE** | `/api/cms/blogs/{item_id}` | Delete Blog | item_id |
| **GET** | `/api/cms/pages` | List Cms Pages | active_only, page, limit, search |
| **POST** | `/api/cms/pages` | Create Cms Page | - |
| **PUT** | `/api/cms/pages/{item_id}` | Update Cms Page | item_id |
| **DELETE** | `/api/cms/pages/{item_id}` | Delete Cms Page | item_id |
| **GET** | `/api/cms/pages/by-slug/{slug}` | Public Cms Page | slug |
| **GET** | `/api/cms/customer-reviews` | List Reviews | active_only, page, limit, search |
| **POST** | `/api/cms/customer-reviews` | Create Review | - |
| **PUT** | `/api/cms/customer-reviews/{item_id}` | Update Review | item_id |
| **DELETE** | `/api/cms/customer-reviews/{item_id}` | Delete Review | item_id |
| **GET** | `/api/cms/help-centre` | List Help | category, active_only, page, limit, search |
| **POST** | `/api/cms/help-centre` | Create Help | - |
| **PUT** | `/api/cms/help-centre/{item_id}` | Update Help | item_id |
| **DELETE** | `/api/cms/help-centre/{item_id}` | Delete Help | item_id |
| **GET** | `/api/cms/policies` | List Policies | page, limit, search |
| **PUT** | `/api/cms/policies` | Upsert Policy | - |
| **GET** | `/api/cms/policies/{slug}` | Get Policy | slug |
| **GET** | `/api/cms/promotional-popups` | List Popups | active_only, page, limit, search |
| **POST** | `/api/cms/promotional-popups` | Create Popup | - |
| **PUT** | `/api/cms/promotional-popups/{item_id}` | Update Popup | item_id |
| **DELETE** | `/api/cms/promotional-popups/{item_id}` | Delete Popup | item_id |
| **GET** | `/api/cms/external-links` | List Links | location, page, limit, search |
| **POST** | `/api/cms/external-links` | Create Link | - |
| **PUT** | `/api/cms/external-links/{item_id}` | Update Link | item_id |
| **DELETE** | `/api/cms/external-links/{item_id}` | Delete Link | item_id |
| **GET** | `/api/cms/footer` | Public Footer | - |
| **GET** | `/api/cms/footer-sections` | List Footer Sections | page, limit, search |
| **POST** | `/api/cms/footer-sections` | Create Footer Section | - |
| **PUT** | `/api/cms/footer-sections/{item_id}` | Update Footer Section | item_id |
| **DELETE** | `/api/cms/footer-sections/{item_id}` | Delete Footer Section | item_id |
| **GET** | `/api/cms/footer-links` | List Footer Links | section_id, page, limit, search |
| **POST** | `/api/cms/footer-links` | Create Footer Link | - |
| **PUT** | `/api/cms/footer-links/{item_id}` | Update Footer Link | item_id |
| **DELETE** | `/api/cms/footer-links/{item_id}` | Delete Footer Link | item_id |
| **GET** | `/api/cms/sitemap` | List Sitemap Entries | page, limit, search |
| **POST** | `/api/cms/sitemap` | Create Sitemap Entry | - |
| **GET** | `/api/cms/sitemap.xml` | Get Sitemap Xml | - |
| **PUT** | `/api/cms/sitemap/{item_id}` | Update Sitemap Entry | item_id |
| **DELETE** | `/api/cms/sitemap/{item_id}` | Delete Sitemap Entry | item_id |

### Wishlist (3 operations)

| Method | Endpoint | Summary | Parameters |
|---|---|---|---|
| **GET** | `/api/wishlist` | User Wishlist | - |
| **POST** | `/api/wishlist/{tour_id}` | Add User Wishlist Item | tour_id |
| **DELETE** | `/api/wishlist/{tour_id}` | Delete User Wishlist Item | tour_id |

---

# 08 — Database Schema & Data Architecture

## 1. Database Engine & ORM Configuration

- **Database Engine**: MySQL 8.0+ or MariaDB using the **InnoDB storage engine** for full ACID compliance and row-level locking.
- **ORM Framework**: SQLAlchemy 2.0 utilizing Declarative Base (`Base = declarative_base()`).
- **Connection Pooling**: Managed via `QueuePool` with configurable pool size, max overflow, and automated pool recycling to prevent stale MySQL disconnects.
- **Character Set**: `utf8mb4` with `utf8mb4_unicode_ci` collation supporting international multi-lingual text and emoji characters.

---

## 2. Relational Schema Statistics

- **Total Tables**: **138 database tables**
- **Migration Revisions**: **170 Alembic migration files** (dating from `2026-06-15` to `2026-10-28`).
- **Foreign Key Density**: High relational integrity with cascading deletion restricted on financial and audit records.

---

## 3. Core Relational Domains

1. **Identity & Access**: `users`, `roles`, `permissions`, `role_permissions`, `user_roles`, `user_sessions`, `login_history`, `audit_logs`.
2. **Geographical Master**: `countries`, `states`, `cities`, `cms_country_pages`, `cms_favourite_countries`.
3. **Tour Catalog**: `tours`, `tour_overviews`, `tour_itineraries`, `tour_pricing`, `tour_calendar`, `tour_unavailable_dates`, `tour_inclusions`, `tour_exclusions`, `tour_highlights`, `tour_gallery_images`, `tour_categories`, `tour_subcategories`.
4. **Tour Versioning**: `tour_versions`, `tour_review_comments`.
5. **Booking Hub**: `bookings`, `booking_travellers`, `booking_optional_activities`, `booking_accommodations`, `booking_extensions`, `booking_status_history`, `booking_communications`, `booking_calendar_events`.
6. **Financial & Checkout**: `payments`, `payment_transactions`, `payment_holds`, `checkout_sessions`, `invoices`, `invoice_items`.
7. **Partner Ledgers**: `suppliers`, `supplier_ledgers`, `supplier_payouts`, `agents`, `agent_ledger`.
8. **Affiliate Engine**: `affiliates`, `affiliate_links`, `affiliate_clicks`, `affiliate_attributions`, `affiliate_commission_rules`, `affiliate_conversions`, `affiliate_payouts`, `affiliate_wallet_transactions`.
9. **CMS & Engagement**: `cms_homepage_banners`, `cms_popular_destinations`, `cms_popular_tours`, `cms_blogs`, `cms_customer_reviews`, `cms_policies`.
10. **Communications & AI**: `conversations`, `messages`, `notifications`, `notification_deliveries`, `chat_faqs`, `chat_sessions`, `chat_messages`, `chat_embeddings`.

The complete schema reference of all 138 tables and columns is cataloged in [`inventories/database-tables.md`](../../inventories/database-tables.md).

---

# Database Table Inventory

**Total Verified Tables:** 138
**Database Engine:** MySQL 8.0+ / MariaDB (InnoDB engine)
**ORM Framework:** SQLAlchemy 2.0 (Declarative Base)
**Migration Engine:** Alembic (170 migration revisions)

| Table Name | Primary Key | Columns | Foreign Keys Count | Foreign Key References |
|---|---|---|---|---|
| `admin_modules` | `id` | 8 | 0 | - |
| `affiliate_attributions` | `id` | 13 | 4 | affiliate_link_id -> affiliate_links.id, affiliate_id -> affiliates.id, affil... |
| `affiliate_clicks` | `id` | 7 | 2 | affiliate_id -> affiliates.id, link_id -> affiliate_links.id |
| `affiliate_commission_rules` | `id` | 18 | 6 | tour_id -> tours.id, updated_by -> users.id, created_by -> users.id, category... |
| `affiliate_conversions` | `id` | 17 | 4 | affiliate_id -> affiliates.id, booking_id -> bookings.id, commission_rule_id ... |
| `affiliate_documents` | `id` | 12 | 2 | reviewed_by -> users.id, affiliate_id -> affiliates.id |
| `affiliate_invoicing` | `id` | 23 | 3 | bank_edit_unlocked_by -> users.id, country_id -> countries.id, affiliate_id -... |
| `affiliate_links` | `id` | 28 | 4 | created_by -> users.id, tour_id -> tours.id, affiliate_id -> affiliates.id, u... |
| `affiliate_marketing_info` | `id` | 9 | 1 | affiliate_id -> affiliates.id |
| `affiliate_payout_items` | `id` | 5 | 2 | payout_id -> affiliate_payouts.id, conversion_id -> affiliate_conversions.id |
| `affiliate_payout_methods` | `id` | 14 | 1 | affiliate_id -> affiliates.id |
| `affiliate_payouts` | `id` | 21 | 5 | payout_method_id -> affiliate_payout_methods.id, approved_by -> users.id, aff... |
| `affiliate_wallet_transactions` | `id` | 11 | 3 | payout_id -> affiliate_payouts.id, commission_id -> affiliate_conversions.id,... |
| `affiliates` | `id` | 23 | 5 | rejected_by -> users.id, approved_by -> users.id, city_id -> cities.id, user_... |
| `agent_business_info` | `id` | 16 | 1 | agent_id -> agents.id |
| `agent_contacts` | `id` | 13 | 1 | agent_id -> agents.id |
| `agent_documents` | `id` | 12 | 2 | agent_id -> agents.id, reviewed_by -> users.id |
| `agent_invoicing` | `id` | 24 | 4 | country_id -> countries.id, bank_edit_unlocked_by -> users.id, agent_id -> ag... |
| `agent_ledgers` | `id` | 14 | 2 | booking_id -> bookings.id, agent_id -> agents.id |
| `agent_payout_items` | `id` | 5 | 2 | payout_id -> agent_payouts.id, ledger_id -> agent_ledgers.id |
| `agent_payouts` | `id` | 18 | 5 | approved_by -> users.id, agent_id -> agents.id, paid_by -> users.id, rejected... |
| `agents` | `id` | 28 | 5 | approved_by -> users.id, rejected_by -> users.id, user_id -> users.id, city_i... |
| `api_settings` | `id` | 8 | 0 | - |
| `app_settings` | `id` | 7 | 0 | - |
| `audit_logs` | `id` | 10 | 1 | actor_user_id -> users.id |
| `booking_accommodations` | `id` | 9 | 2 | booking_id -> bookings.id, tour_accommodation_extra_id -> tour_accommodation_... |
| `booking_calendar_events` | `id` | 13 | 1 | booking_id -> bookings.id |
| `booking_communications` | `id` | 9 | 2 | booking_id -> bookings.id, sender_user_id -> users.id |
| `booking_conversations` | `id` | 12 | 3 | supplier_user_id -> users.id, booking_id -> bookings.id, initiator_user_id ->... |
| `booking_extensions` | `id` | 9 | 3 | tour_extension_id -> tour_extensions.id, booking_id -> bookings.id, extension... |
| `booking_messages` | `id` | 11 | 2 | sender_user_id -> users.id, conversation_id -> booking_conversations.id |
| `booking_modification_requests` | `id` | 14 | 3 | requester_user_id -> users.id, reviewed_by -> users.id, booking_id -> booking... |
| `booking_optional_activities` | `id` | 8 | 2 | booking_id -> bookings.id, tour_optional_activity_id -> tour_optional_activit... |
| `booking_status_history` | `id` | 9 | 2 | changed_by_user_id -> users.id, booking_id -> bookings.id |
| `booking_travellers` | `id` | 20 | 1 | booking_id -> bookings.id |
| `bookings` | `id` | 107 | 14 | affiliate_id -> affiliates.id, agent_id -> agents.id, supplier_id -> supplier... |
| `cancellation_requests` | `id` | 16 | 3 | booking_id -> bookings.id, customer_id -> customers.id, reviewed_by -> users.id |
| `chat_embeddings` | `id` | 8 | 0 | - |
| `chat_faqs` | `id` | 9 | 0 | - |
| `chat_feedback` | `id` | 7 | 2 | message_id -> chat_messages.id, session_id -> chat_sessions.id |
| `chat_messages` | `id` | 5 | 1 | session_id -> chat_sessions.id |
| `chat_sessions` | `id` | 5 | 0 | - |
| `checkout_sessions` | `id` | 13 | 5 | customer_id -> customers.id, user_id -> users.id, tour_id -> tours.id, bookin... |
| `cities` | `id` | 7 | 2 | state_id -> states.id, country_id -> countries.id |
| `cms_blogs` | `id` | 19 | 1 | created_by -> users.id |
| `cms_country_pages` | `id` | 13 | 1 | country_id -> countries.id |
| `cms_customer_reviews` | `id` | 11 | 0 | - |
| `cms_external_links` | `id` | 9 | 0 | - |
| `cms_favourite_countries` | `id` | 10 | 1 | country_id -> countries.id |
| `cms_footer_links` | `id` | 9 | 1 | section_id -> cms_footer_sections.id |
| `cms_footer_sections` | `id` | 6 | 0 | - |
| `cms_handpicked_tours` | `id` | 5 | 1 | tour_id -> tours.id |
| `cms_help_centre` | `id` | 8 | 0 | - |
| `cms_homepage_banners` | `id` | 11 | 0 | - |
| `cms_homepage_content_blocks` | `id` | 5 | 0 | - |
| `cms_pages` | `id` | 12 | 1 | footer_section_id -> cms_footer_sections.id |
| `cms_policies` | `id` | 7 | 0 | - |
| `cms_popular_destinations` | `id` | 13 | 2 | country_id -> countries.id, city_id -> cities.id |
| `cms_popular_tours` | `id` | 5 | 1 | tour_id -> tours.id |
| `cms_promotional_popups` | `id` | 13 | 0 | - |
| `cms_sitemap_entries` | `id` | 8 | 0 | - |
| `cms_tours_on_deals` | `id` | 9 | 1 | tour_id -> tours.id |
| `contact_messages` | `id` | 10 | 0 | - |
| `conversations` | `id` | 10 | 1 | participant_user_id -> users.id |
| `countries` | `id` | 10 | 0 | - |
| `currencies` | `id` | 7 | 0 | - |
| `customer_cancellation_requests` | `id` | 10 | 3 | reviewed_by -> users.id, booking_id -> bookings.id, customer_id -> customers.id |
| `customer_communications` | `id` | 10 | 3 | sent_by_user_id -> users.id, customer_id -> customers.id, booking_id -> booki... |
| `customer_saved_travellers` | `id` | 13 | 1 | customer_id -> customers.id |
| `customer_wishlist_items` | `id` | 5 | 2 | tour_id -> tours.id, user_id -> users.id |
| `customers` | `id` | 48 | 5 | user_id -> users.id, city_id -> cities.id, blocked_by -> users.id, country_id... |
| `email_logs` | `id` | 10 | 0 | - |
| `email_templates` | `id` | 7 | 0 | - |
| `external_affiliate_clicks` | `id` | 16 | 4 | tourvaa_country_id -> countries.id, agent_id -> agents.id, tourvaa_city_id ->... |
| `external_destination_mappings` | `id` | 17 | 3 | tourvaa_city_id -> cities.id, tourvaa_state_id -> states.id, tourvaa_country_... |
| `external_providers` | `id` | 16 | 0 | - |
| `invoice_items` | `id` | 9 | 1 | invoice_id -> invoices.id |
| `invoices` | `id` | 24 | 4 | booking_id -> bookings.id, payment_id -> payments.id, created_by -> users.id,... |
| `login_history` | `id` | 12 | 1 | user_id -> users.id |
| `message_replies` | `id` | 6 | 2 | sender_user_id -> users.id, communication_id -> booking_communications.id |
| `messages` | `id` | 10 | 2 | sender_user_id -> users.id, conversation_id -> conversations.id |
| `newsletter_subscribers` | `id` | 4 | 0 | - |
| `notification_deliveries` | `id` | 21 | 0 | - |
| `notification_logs` | `id` | 6 | 1 | notification_id -> notifications.id |
| `notifications` | `id` | 19 | 1 | user_id -> users.id |
| `payment_holds` | `id` | 10 | 2 | payment_id -> payments.id, booking_id -> bookings.id |
| `payment_settings` | `id` | 17 | 0 | - |
| `payment_transactions` | `id` | 10 | 3 | booking_id -> bookings.id, payment_id -> payments.id, created_by -> users.id |
| `payments` | `id` | 26 | 3 | customer_id -> customers.id, created_by -> users.id, booking_id -> bookings.id |
| `permissions` | `id` | 8 | 0 | - |
| `push_delivery_logs` | `id` | 13 | 3 | recipient_user_id -> users.id, notification_id -> notifications.id, subscript... |
| `push_subscriptions` | `id` | 12 | 1 | user_id -> users.id |
| `refund_rules` | `id` | 8 | 1 | tour_id -> tours.id |
| `report_schedules` | `id` | 8 | 1 | created_by -> users.id |
| `role_permissions` | `id` | 3 | 2 | permission_id -> permissions.id, role_id -> roles.id |
| `roles` | `id` | 6 | 0 | - |
| `smtp_settings` | `id` | 17 | 0 | - |
| `states` | `id` | 7 | 1 | country_id -> countries.id |
| `supplier_approval_history` | `id` | 7 | 2 | supplier_id -> suppliers.id, changed_by -> users.id |
| `supplier_business_info` | `id` | 15 | 1 | supplier_id -> suppliers.id |
| `supplier_contacts` | `id` | 13 | 1 | supplier_id -> suppliers.id |
| `supplier_documents` | `id` | 12 | 2 | supplier_id -> suppliers.id, reviewed_by -> users.id |
| `supplier_invoicing` | `id` | 24 | 4 | supplier_id -> suppliers.id, bank_edit_unlocked_by -> users.id, bank_country_... |
| `supplier_ledgers` | `id` | 14 | 2 | supplier_id -> suppliers.id, booking_id -> bookings.id |
| `supplier_payout_items` | `id` | 5 | 2 | payout_id -> supplier_payouts.id, ledger_id -> supplier_ledgers.id |
| `supplier_payouts` | `id` | 15 | 4 | paid_by -> users.id, initiated_by -> users.id, approved_by -> users.id, suppl... |
| `supplier_vehicles` | `id` | 17 | 2 | reviewed_by -> users.id, supplier_id -> suppliers.id |
| `suppliers` | `id` | 23 | 5 | rejected_by -> users.id, approved_by -> users.id, city_id -> cities.id, count... |
| `tour_accommodation_extras` | `id` | 14 | 1 | tour_id -> tours.id |
| `tour_availability_configs` | `id` | 15 | 1 | tour_id -> tours.id |
| `tour_calendar` | `id` | 11 | 1 | tour_id -> tours.id |
| `tour_categories` | `id` | 8 | 0 | - |
| `tour_date_prices` | `id` | 8 | 1 | tour_id -> tours.id |
| `tour_discount_history` | `id` | 12 | 2 | changed_by -> users.id, discount_id -> tour_discounts.id |
| `tour_discount_redemptions` | `id` | 6 | 2 | discount_id -> tour_discounts.id, booking_id -> bookings.id |
| `tour_discounts` | `id` | 19 | 3 | tour_id -> tours.id, country_id -> countries.id, category_id -> tour_categori... |
| `tour_exclusions` | `id` | 9 | 1 | tour_id -> tours.id |
| `tour_extensions` | `id` | 14 | 2 | tour_id -> tours.id, extension_tour_id -> tours.id |
| `tour_gallery_images` | `id` | 11 | 1 | tour_id -> tours.id |
| `tour_group_discount_tiers` | `id` | 10 | 1 | tour_id -> tours.id |
| `tour_highlights` | `id` | 9 | 1 | tour_id -> tours.id |
| `tour_inclusions` | `id` | 9 | 1 | tour_id -> tours.id |
| `tour_itineraries` | `id` | 25 | 1 | tour_id -> tours.id |
| `tour_optional_activities` | `id` | 15 | 1 | tour_id -> tours.id |
| `tour_overviews` | `id` | 20 | 1 | tour_id -> tours.id |
| `tour_pricing` | `id` | 19 | 1 | tour_id -> tours.id |
| `tour_review_comments` | `id` | 13 | 4 | tour_id -> tours.id, resolved_by -> users.id, version_id -> tour_versions.id,... |
| `tour_reviews` | `id` | 9 | 3 | customer_id -> customers.id, booking_id -> bookings.id, tour_id -> tours.id |
| `tour_similar_tours` | `id` | 6 | 2 | tour_id -> tours.id, similar_tour_id -> tours.id |
| `tour_subcategories` | `id` | 9 | 1 | category_id -> tour_categories.id |
| `tour_subcategory_map` | `id` | 4 | 2 | tour_id -> tours.id, subcategory_id -> tour_subcategories.id |
| `tour_unavailable_dates` | `id` | 6 | 1 | tour_id -> tours.id |
| `tour_versions` | `id` | 12 | 3 | tour_id -> tours.id, reviewed_by -> users.id, submitted_by -> users.id |
| `tours` | `id` | 58 | 7 | state_id -> states.id, category_id -> tour_categories.id, city_id -> cities.i... |
| `user_roles` | `id` | 4 | 2 | user_id -> users.id, role_id -> roles.id |
| `user_sessions` | `id` | 10 | 1 | user_id -> users.id |
| `user_status_history` | `id` | 7 | 2 | changed_by -> users.id, user_id -> users.id |
| `users` | `id` | 44 | 3 | role_id -> roles.id, deactivated_by -> users.id, admin_verified_by -> users.id |

## Detailed Table Schema Reference

### `admin_modules`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `name` | `VARCHAR(100)` | False | False | - |
| `slug` | `VARCHAR(100)` | False | False | - |
| `description` | `VARCHAR(255)` | False | False |  |
| `is_active` | `BOOLEAN` | False | False | True |
| `is_system` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `affiliate_attributions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `affiliate_id` | `INTEGER` | False | False | - |
| `affiliate_link_id` | `INTEGER` | False | False | - |
| `affiliate_click_id` | `INTEGER` | True | False | - |
| `visitor_id` | `VARCHAR(64)` | False | False | - |
| `session_id` | `VARCHAR(64)` | True | False | - |
| `booking_id` | `INTEGER` | True | False | - |
| `attribution_model` | `VARCHAR(20)` | False | False | last_click |
| `attributed_at` | `DATETIME` | True | False | - |
| `expires_at` | `DATETIME` | False | False | - |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `affiliate_link_id` references `affiliate_links.id`
- Column `affiliate_id` references `affiliates.id`
- Column `affiliate_click_id` references `affiliate_clicks.id`
- Column `booking_id` references `bookings.id`

### `affiliate_clicks`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `link_id` | `INTEGER` | False | False | - |
| `affiliate_id` | `INTEGER` | False | False | - |
| `ip_address` | `VARCHAR(50)` | True | False | - |
| `user_agent` | `VARCHAR(500)` | True | False | - |
| `referrer` | `VARCHAR(500)` | True | False | - |
| `clicked_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `affiliate_id` references `affiliates.id`
- Column `link_id` references `affiliate_links.id`

### `affiliate_commission_rules`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `name` | `VARCHAR(150)` | True | False | - |
| `affiliate_id` | `INTEGER` | True | False | - |
| `tour_id` | `INTEGER` | True | False | - |
| `category_id` | `INTEGER` | True | False | - |
| `affiliate_link_id` | `INTEGER` | True | False | - |
| `commission_type` | `VARCHAR(20)` | False | False | percentage |
| `percentage` | `NUMERIC(5, 2)` | False | False | 0 |
| `fixed_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `valid_from` | `DATETIME` | True | False | - |
| `valid_until` | `DATETIME` | True | False | - |
| `priority` | `INTEGER` | False | False | 0 |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_by` | `INTEGER` | True | False | - |
| `updated_by` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`
- Column `updated_by` references `users.id`
- Column `created_by` references `users.id`
- Column `category_id` references `tour_categories.id`
- Column `affiliate_id` references `affiliates.id`
- Column `affiliate_link_id` references `affiliate_links.id`

### `affiliate_conversions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `link_id` | `INTEGER` | False | False | - |
| `affiliate_id` | `INTEGER` | False | False | - |
| `booking_id` | `INTEGER` | False | False | - |
| `commission_rule_id` | `INTEGER` | True | False | - |
| `booking_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `eligible_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `commission_percentage` | `NUMERIC(5, 2)` | False | False | 0 |
| `commission_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `original_commission` | `NUMERIC(12, 2)` | True | False | - |
| `adjustment_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `final_commission` | `NUMERIC(12, 2)` | True | False | - |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `status` | `VARCHAR(30)` | False | False | pending |
| `approved_at` | `DATETIME` | True | False | - |
| `available_at` | `DATETIME` | True | False | - |
| `converted_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `affiliate_id` references `affiliates.id`
- Column `booking_id` references `bookings.id`
- Column `commission_rule_id` references `affiliate_commission_rules.id`
- Column `link_id` references `affiliate_links.id`

### `affiliate_documents`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `affiliate_id` | `INTEGER` | False | False | - |
| `document_type` | `VARCHAR(100)` | False | False | - |
| `document_name` | `VARCHAR(150)` | False | False | - |
| `file_path` | `VARCHAR(255)` | False | False | - |
| `file_size` | `INTEGER` | False | False | 0 |
| `mime_type` | `VARCHAR(100)` | False | False |  |
| `status` | `VARCHAR(20)` | False | False | pending |
| `rejection_reason` | `VARCHAR(255)` | True | False | - |
| `uploaded_at` | `DATETIME` | True | False | - |
| `reviewed_at` | `DATETIME` | True | False | - |
| `reviewed_by` | `INTEGER` | True | False | - |

**Foreign Keys:**
- Column `reviewed_by` references `users.id`
- Column `affiliate_id` references `affiliates.id`

### `affiliate_invoicing`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `affiliate_id` | `INTEGER` | False | False | - |
| `contact_name` | `VARCHAR(150)` | False | False |  |
| `email` | `VARCHAR(150)` | False | False |  |
| `phone` | `VARCHAR(30)` | False | False |  |
| `preferred_payment_method` | `VARCHAR(30)` | False | False |  |
| `account_name` | `VARCHAR(150)` | False | False |  |
| `account_number` | `VARCHAR(100)` | False | False |  |
| `bank_name` | `VARCHAR(150)` | False | False |  |
| `bank_branch` | `VARCHAR(150)` | False | False |  |
| `swift_code` | `VARCHAR(50)` | False | False |  |
| `iban` | `VARCHAR(100)` | False | False |  |
| `country_id` | `INTEGER` | True | False | - |
| `tax_number` | `VARCHAR(100)` | False | False |  |
| `billing_address` | `TEXT` | True | False | - |
| `billing_city` | `VARCHAR(100)` | False | False |  |
| `billing_state` | `VARCHAR(100)` | False | False |  |
| `billing_postal_code` | `VARCHAR(30)` | False | False |  |
| `bank_edit_requested_at` | `DATETIME` | True | False | - |
| `bank_edit_unlocked_at` | `DATETIME` | True | False | - |
| `bank_edit_unlocked_by` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `bank_edit_unlocked_by` references `users.id`
- Column `country_id` references `countries.id`
- Column `affiliate_id` references `affiliates.id`

### `affiliate_links`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `affiliate_id` | `INTEGER` | False | False | - |
| `ref_code` | `VARCHAR(60)` | False | False | - |
| `destination_url` | `VARCHAR(500)` | True | False | - |
| `label` | `VARCHAR(120)` | True | False | - |
| `is_active` | `BOOLEAN` | False | False | True |
| `link_type` | `VARCHAR(20)` | False | False | custom |
| `tour_id` | `INTEGER` | True | False | - |
| `campaign_name` | `VARCHAR(150)` | True | False | - |
| `utm_source` | `VARCHAR(100)` | True | False | - |
| `utm_medium` | `VARCHAR(100)` | True | False | - |
| `utm_campaign` | `VARCHAR(100)` | True | False | - |
| `utm_content` | `VARCHAR(100)` | True | False | - |
| `utm_term` | `VARCHAR(100)` | True | False | - |
| `custom_alias` | `VARCHAR(100)` | True | False | - |
| `commission_type_override` | `VARCHAR(20)` | True | False | - |
| `commission_percentage_override` | `NUMERIC(5, 2)` | True | False | - |
| `commission_fixed_override` | `NUMERIC(12, 2)` | True | False | - |
| `attribution_model` | `VARCHAR(20)` | False | False | last_click |
| `attribution_window_days` | `INTEGER` | False | False | 30 |
| `valid_from` | `DATETIME` | True | False | - |
| `valid_until` | `DATETIME` | True | False | - |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_by` | `INTEGER` | True | False | - |
| `updated_by` | `INTEGER` | True | False | - |
| `deleted_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `created_by` references `users.id`
- Column `tour_id` references `tours.id`
- Column `affiliate_id` references `affiliates.id`
- Column `updated_by` references `users.id`

### `affiliate_marketing_info`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `affiliate_id` | `INTEGER` | False | False | - |
| `promotion_methods` | `TEXT` | False | False |  |
| `estimated_monthly_bookings` | `INTEGER` | False | False | 0 |
| `existing_audience_size` | `INTEGER` | False | False | 0 |
| `social_media_profiles` | `TEXT` | False | False |  |
| `existing_travel_platforms_used` | `TEXT` | False | False |  |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `affiliate_id` references `affiliates.id`

### `affiliate_payout_items`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `payout_id` | `INTEGER` | False | False | - |
| `conversion_id` | `INTEGER` | False | False | - |
| `amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `payout_id` references `affiliate_payouts.id`
- Column `conversion_id` references `affiliate_conversions.id`

### `affiliate_payout_methods`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `affiliate_id` | `INTEGER` | False | False | - |
| `method_type` | `VARCHAR(30)` | False | False | bank_transfer |
| `account_holder_name` | `VARCHAR(150)` | False | False |  |
| `bank_name` | `VARCHAR(150)` | False | False |  |
| `account_number` | `VARCHAR(100)` | False | False |  |
| `ifsc` | `VARCHAR(30)` | False | False |  |
| `swift_code` | `VARCHAR(30)` | False | False |  |
| `bank_country` | `VARCHAR(100)` | False | False |  |
| `paypal_email` | `VARCHAR(150)` | False | False |  |
| `is_default` | `BOOLEAN` | False | False | False |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `affiliate_id` references `affiliates.id`

### `affiliate_payouts`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `payout_code` | `VARCHAR(30)` | True | False | - |
| `affiliate_id` | `INTEGER` | False | False | - |
| `payout_method_id` | `INTEGER` | True | False | - |
| `total_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `payment_method` | `VARCHAR(50)` | False | False | bank_transfer |
| `reference_number` | `VARCHAR(150)` | True | False | - |
| `status` | `VARCHAR(30)` | False | False | pending |
| `notes` | `TEXT` | True | False | - |
| `requested_at` | `DATETIME` | True | False | - |
| `approved_at` | `DATETIME` | True | False | - |
| `approved_by` | `INTEGER` | True | False | - |
| `rejected_at` | `DATETIME` | True | False | - |
| `rejected_by` | `INTEGER` | True | False | - |
| `rejection_reason` | `VARCHAR(255)` | True | False | - |
| `processing_at` | `DATETIME` | True | False | - |
| `initiated_by` | `INTEGER` | True | False | - |
| `paid_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `payout_method_id` references `affiliate_payout_methods.id`
- Column `approved_by` references `users.id`
- Column `affiliate_id` references `affiliates.id`
- Column `initiated_by` references `users.id`
- Column `rejected_by` references `users.id`

### `affiliate_wallet_transactions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `affiliate_id` | `INTEGER` | False | False | - |
| `commission_id` | `INTEGER` | True | False | - |
| `payout_id` | `INTEGER` | True | False | - |
| `transaction_type` | `VARCHAR(30)` | False | False | - |
| `amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `reference_type` | `VARCHAR(30)` | True | False | - |
| `reference_id` | `INTEGER` | True | False | - |
| `description` | `VARCHAR(255)` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `payout_id` references `affiliate_payouts.id`
- Column `commission_id` references `affiliate_conversions.id`
- Column `affiliate_id` references `affiliates.id`

### `affiliates`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `user_id` | `INTEGER` | True | False | - |
| `affiliate_code` | `VARCHAR(30)` | True | False | - |
| `business_type` | `VARCHAR(75)` | False | False |  |
| `name` | `VARCHAR(150)` | False | False | - |
| `email` | `VARCHAR(150)` | False | False | - |
| `phone` | `VARCHAR(30)` | False | False |  |
| `website_url` | `VARCHAR(255)` | False | False |  |
| `country_id` | `INTEGER` | True | False | - |
| `city_id` | `INTEGER` | True | False | - |
| `status` | `VARCHAR(20)` | False | False | inactive |
| `approval_status` | `VARCHAR(30)` | False | False | pending |
| `commission_percentage` | `NUMERIC(5, 2)` | False | False | 0 |
| `rejection_reason` | `VARCHAR(255)` | True | False | - |
| `admin_comments` | `TEXT` | True | False | - |
| `api_link` | `VARCHAR(255)` | False | False |  |
| `approved_at` | `DATETIME` | True | False | - |
| `approved_by` | `INTEGER` | True | False | - |
| `rejected_at` | `DATETIME` | True | False | - |
| `rejected_by` | `INTEGER` | True | False | - |
| `commission_accepted_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `rejected_by` references `users.id`
- Column `approved_by` references `users.id`
- Column `city_id` references `cities.id`
- Column `user_id` references `users.id`
- Column `country_id` references `countries.id`

### `agent_business_info`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `agent_id` | `INTEGER` | False | False | - |
| `years_in_business` | `INTEGER` | False | False | 0 |
| `certificate_of_incorporation` | `VARCHAR(255)` | False | False |  |
| `monthly_customers_count` | `INTEGER` | False | False | 0 |
| `target_market` | `VARCHAR(255)` | False | False |  |
| `destinations_sold` | `TEXT` | False | False |  |
| `iata_registration_number` | `VARCHAR(100)` | False | False |  |
| `gst_tax_number` | `VARCHAR(100)` | False | False |  |
| `trading_name` | `VARCHAR(150)` | False | False |  |
| `business_email` | `VARCHAR(150)` | False | False |  |
| `website_url` | `VARCHAR(255)` | False | False |  |
| `business_registration_number` | `VARCHAR(100)` | False | False |  |
| `approval_status` | `VARCHAR(30)` | False | False | pending |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `agent_id` references `agents.id`

### `agent_contacts`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `agent_id` | `INTEGER` | False | False | - |
| `contact_name` | `VARCHAR(150)` | False | False | - |
| `first_name` | `VARCHAR(75)` | False | False |  |
| `last_name` | `VARCHAR(75)` | False | False |  |
| `designation` | `VARCHAR(100)` | False | False |  |
| `phone` | `VARCHAR(30)` | False | False |  |
| `email` | `VARCHAR(150)` | False | False |  |
| `alternate_phone` | `VARCHAR(30)` | False | False |  |
| `preferred_contact_method` | `VARCHAR(20)` | False | False |  |
| `is_primary` | `BOOLEAN` | False | False | False |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `agent_id` references `agents.id`

### `agent_documents`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `agent_id` | `INTEGER` | False | False | - |
| `document_type` | `VARCHAR(100)` | False | False | - |
| `document_name` | `VARCHAR(150)` | False | False | - |
| `file_path` | `VARCHAR(255)` | False | False | - |
| `file_size` | `INTEGER` | False | False | 0 |
| `mime_type` | `VARCHAR(100)` | False | False |  |
| `status` | `VARCHAR(20)` | False | False | pending |
| `rejection_reason` | `VARCHAR(255)` | True | False | - |
| `uploaded_at` | `DATETIME` | True | False | - |
| `reviewed_at` | `DATETIME` | True | False | - |
| `reviewed_by` | `INTEGER` | True | False | - |

**Foreign Keys:**
- Column `agent_id` references `agents.id`
- Column `reviewed_by` references `users.id`

### `agent_invoicing`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `agent_id` | `INTEGER` | False | False | - |
| `contact_name` | `VARCHAR(150)` | False | False |  |
| `email` | `VARCHAR(150)` | False | False |  |
| `phone` | `VARCHAR(30)` | False | False |  |
| `preferred_payment_method` | `VARCHAR(30)` | False | False |  |
| `account_name` | `VARCHAR(150)` | False | False |  |
| `account_number` | `VARCHAR(100)` | False | False |  |
| `bank_name` | `VARCHAR(150)` | False | False |  |
| `bank_branch` | `VARCHAR(150)` | False | False |  |
| `swift_code` | `VARCHAR(50)` | False | False |  |
| `iban` | `VARCHAR(100)` | False | False |  |
| `country_id` | `INTEGER` | True | False | - |
| `bank_country_id` | `INTEGER` | True | False | - |
| `tax_number` | `VARCHAR(100)` | False | False |  |
| `billing_address` | `TEXT` | True | False | - |
| `billing_city` | `VARCHAR(100)` | False | False |  |
| `billing_state` | `VARCHAR(100)` | False | False |  |
| `billing_postal_code` | `VARCHAR(30)` | False | False |  |
| `bank_edit_requested_at` | `DATETIME` | True | False | - |
| `bank_edit_unlocked_at` | `DATETIME` | True | False | - |
| `bank_edit_unlocked_by` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `country_id` references `countries.id`
- Column `bank_edit_unlocked_by` references `users.id`
- Column `agent_id` references `agents.id`
- Column `bank_country_id` references `countries.id`

### `agent_ledgers`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `agent_id` | `INTEGER` | False | False | - |
| `booking_id` | `INTEGER` | False | False | - |
| `gross_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `commission_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `commission_percentage` | `NUMERIC(5, 2)` | False | False | 0 |
| `net_payable` | `NUMERIC(12, 2)` | False | False | 0 |
| `amount_paid` | `NUMERIC(12, 2)` | False | False | 0 |
| `amount_pending` | `NUMERIC(12, 2)` | False | False | 0 |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `status` | `VARCHAR(30)` | False | False | pending |
| `notes` | `TEXT` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `booking_id` references `bookings.id`
- Column `agent_id` references `agents.id`

### `agent_payout_items`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `payout_id` | `INTEGER` | False | False | - |
| `ledger_id` | `INTEGER` | False | False | - |
| `amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `payout_id` references `agent_payouts.id`
- Column `ledger_id` references `agent_ledgers.id`

### `agent_payouts`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `payout_code` | `VARCHAR(30)` | True | False | - |
| `agent_id` | `INTEGER` | False | False | - |
| `total_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `payment_method` | `VARCHAR(50)` | False | False | bank_transfer |
| `reference_number` | `VARCHAR(150)` | True | False | - |
| `status` | `VARCHAR(30)` | False | False | pending |
| `notes` | `TEXT` | True | False | - |
| `initiated_by` | `INTEGER` | True | False | - |
| `approved_by` | `INTEGER` | True | False | - |
| `rejected_by` | `INTEGER` | True | False | - |
| `rejected_at` | `DATETIME` | True | False | - |
| `rejection_reason` | `VARCHAR(255)` | True | False | - |
| `paid_by` | `INTEGER` | True | False | - |
| `paid_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `approved_by` references `users.id`
- Column `agent_id` references `agents.id`
- Column `paid_by` references `users.id`
- Column `rejected_by` references `users.id`
- Column `initiated_by` references `users.id`

### `agents`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `user_id` | `INTEGER` | True | False | - |
| `agent_code` | `VARCHAR(30)` | True | False | - |
| `agent_name` | `VARCHAR(150)` | False | False | - |
| `agent_type` | `VARCHAR(75)` | False | False |  |
| `country_id` | `INTEGER` | True | False | - |
| `city_id` | `INTEGER` | True | False | - |
| `currency` | `VARCHAR(10)` | True | False | - |
| `years_in_operation` | `INTEGER` | False | False | 0 |
| `status` | `VARCHAR(20)` | False | False | inactive |
| `approval_status` | `VARCHAR(30)` | False | False | pending |
| `rejection_reason` | `VARCHAR(255)` | True | False | - |
| `admin_comments` | `TEXT` | True | False | - |
| `pending_requirements` | `TEXT` | True | False | - |
| `discount_type` | `VARCHAR(20)` | True | False | - |
| `discount_value` | `NUMERIC(12, 2)` | False | False | 0 |
| `commission_request_type` | `VARCHAR(20)` | True | False | - |
| `commission_request_value` | `NUMERIC(12, 2)` | True | False | - |
| `commission_request_status` | `VARCHAR(20)` | True | False | - |
| `commission_requested_at` | `DATETIME` | True | False | - |
| `commission_reviewed_at` | `DATETIME` | True | False | - |
| `approved_at` | `DATETIME` | True | False | - |
| `approved_by` | `INTEGER` | True | False | - |
| `rejected_at` | `DATETIME` | True | False | - |
| `rejected_by` | `INTEGER` | True | False | - |
| `commission_accepted_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `approved_by` references `users.id`
- Column `rejected_by` references `users.id`
- Column `user_id` references `users.id`
- Column `city_id` references `cities.id`
- Column `country_id` references `countries.id`

### `api_settings`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `api_name` | `VARCHAR(100)` | False | False | - |
| `api_key` | `TEXT` | True | False | - |
| `api_secret` | `TEXT` | True | False | - |
| `api_url` | `TEXT` | True | False | - |
| `is_enabled` | `BOOLEAN` | False | False | False |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `app_settings`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `key` | `VARCHAR(100)` | False | False | - |
| `value` | `TEXT` | True | False | - |
| `label` | `VARCHAR(150)` | False | False | - |
| `group` | `VARCHAR(80)` | False | False | general |
| `is_public` | `BOOLEAN` | True | False | False |
| `updated_at` | `DATETIME` | True | False | - |

### `audit_logs`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `actor_user_id` | `INTEGER` | True | False | - |
| `action` | `VARCHAR(100)` | False | False | - |
| `entity_type` | `VARCHAR(100)` | False | False | - |
| `entity_id` | `INTEGER` | True | False | - |
| `old_values` | `JSON` | True | False | - |
| `new_values` | `JSON` | True | False | - |
| `ip_address` | `VARCHAR(100)` | True | False | - |
| `user_agent` | `VARCHAR(255)` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `actor_user_id` references `users.id`

### `booking_accommodations`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `booking_id` | `INTEGER` | False | False | - |
| `tour_accommodation_extra_id` | `INTEGER` | True | False | - |
| `accommodation_name_snapshot` | `VARCHAR(255)` | False | False | - |
| `quantity` | `INTEGER` | False | False | 1 |
| `price_type` | `VARCHAR(30)` | False | False | per_person |
| `unit_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `total_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `booking_id` references `bookings.id`
- Column `tour_accommodation_extra_id` references `tour_accommodation_extras.id`

### `booking_calendar_events`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `booking_id` | `INTEGER` | False | False | - |
| `provider` | `VARCHAR(30)` | False | False | internal |
| `external_event_id` | `VARCHAR(255)` | True | False | - |
| `event_url` | `VARCHAR(500)` | True | False | - |
| `ical_uid` | `VARCHAR(100)` | True | False | - |
| `ics_file_path` | `VARCHAR(255)` | True | False | - |
| `sync_status` | `VARCHAR(30)` | False | False | synced |
| `sync_error` | `TEXT` | True | False | - |
| `retry_count` | `INTEGER` | False | False | 0 |
| `last_synced_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `booking_id` references `bookings.id`

### `booking_communications`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `booking_id` | `INTEGER` | False | False | - |
| `sender_user_id` | `INTEGER` | True | False | - |
| `sender_type` | `VARCHAR(30)` | False | False | admin |
| `message_type` | `VARCHAR(30)` | False | False | admin_message |
| `subject` | `VARCHAR(255)` | False | False |  |
| `message` | `TEXT` | False | False | - |
| `visibility` | `VARCHAR(30)` | False | False | internal |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `booking_id` references `bookings.id`
- Column `sender_user_id` references `users.id`

### `booking_conversations`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `booking_id` | `INTEGER` | False | False | - |
| `initiator_role` | `VARCHAR(20)` | False | False | - |
| `initiator_user_id` | `INTEGER` | False | False | - |
| `supplier_user_id` | `INTEGER` | False | False | - |
| `status` | `VARCHAR(20)` | False | False | open |
| `last_message_at` | `DATETIME` | True | False | - |
| `last_message_preview` | `VARCHAR(300)` | True | False | - |
| `initiator_unread_count` | `INTEGER` | False | False | 0 |
| `supplier_unread_count` | `INTEGER` | False | False | 0 |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `supplier_user_id` references `users.id`
- Column `booking_id` references `bookings.id`
- Column `initiator_user_id` references `users.id`

### `booking_extensions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `booking_id` | `INTEGER` | False | False | - |
| `tour_extension_id` | `INTEGER` | True | False | - |
| `extension_tour_id` | `INTEGER` | True | False | - |
| `extension_name_snapshot` | `VARCHAR(255)` | False | False | - |
| `quantity` | `INTEGER` | False | False | 1 |
| `unit_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `total_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_extension_id` references `tour_extensions.id`
- Column `booking_id` references `bookings.id`
- Column `extension_tour_id` references `tours.id`

### `booking_messages`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `conversation_id` | `INTEGER` | False | False | - |
| `sender_user_id` | `INTEGER` | True | False | - |
| `sender_role` | `VARCHAR(20)` | False | False | - |
| `recipient_role` | `VARCHAR(20)` | True | False | - |
| `body` | `TEXT` | False | False | - |
| `is_deleted` | `BOOLEAN` | False | False | False |
| `deleted_at` | `DATETIME` | True | False | - |
| `delivered_at` | `DATETIME` | True | False | - |
| `read_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `sender_user_id` references `users.id`
- Column `conversation_id` references `booking_conversations.id`

### `booking_modification_requests`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `booking_id` | `INTEGER` | False | False | - |
| `status` | `VARCHAR(20)` | False | False | pending |
| `requester_user_id` | `INTEGER` | False | False | - |
| `requester_type` | `VARCHAR(30)` | False | False | - |
| `proposed_changes` | `JSON` | False | False | - |
| `original_values` | `JSON` | False | False | - |
| `reason` | `TEXT` | True | False | - |
| `reviewed_by` | `INTEGER` | True | False | - |
| `decision_reason` | `TEXT` | True | False | - |
| `decision_history` | `JSON` | True | False | - |
| `reviewed_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `requester_user_id` references `users.id`
- Column `reviewed_by` references `users.id`
- Column `booking_id` references `bookings.id`

### `booking_optional_activities`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `booking_id` | `INTEGER` | False | False | - |
| `tour_optional_activity_id` | `INTEGER` | True | False | - |
| `activity_name_snapshot` | `VARCHAR(255)` | False | False | - |
| `quantity` | `INTEGER` | False | False | 1 |
| `unit_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `total_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `booking_id` references `bookings.id`
- Column `tour_optional_activity_id` references `tour_optional_activities.id`

### `booking_status_history`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `booking_id` | `INTEGER` | False | False | - |
| `old_status` | `VARCHAR(30)` | True | False | - |
| `new_status` | `VARCHAR(30)` | False | False | - |
| `changed_by_user_id` | `INTEGER` | True | False | - |
| `change_source` | `VARCHAR(30)` | False | False | admin |
| `reason` | `TEXT` | True | False | - |
| `metadata_json` | `JSON` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `changed_by_user_id` references `users.id`
- Column `booking_id` references `bookings.id`

### `booking_travellers`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `booking_id` | `INTEGER` | False | False | - |
| `traveller_type` | `VARCHAR(20)` | False | False | - |
| `first_name` | `VARCHAR(100)` | False | False |  |
| `last_name` | `VARCHAR(100)` | False | False |  |
| `full_name` | `VARCHAR(220)` | False | False |  |
| `date_of_birth` | `DATETIME` | True | False | - |
| `age` | `INTEGER` | True | False | - |
| `gender` | `VARCHAR(30)` | True | False | - |
| `nationality` | `VARCHAR(100)` | True | False | - |
| `passport_number` | `VARCHAR(100)` | True | False | - |
| `passport_expiry_date` | `DATETIME` | True | False | - |
| `email` | `VARCHAR(150)` | True | False | - |
| `phone` | `VARCHAR(50)` | True | False | - |
| `is_primary_contact` | `INTEGER` | False | False | 0 |
| `special_requirements` | `TEXT` | True | False | - |
| `pickup_location` | `VARCHAR(255)` | True | False | - |
| `emergency_contact` | `VARCHAR(150)` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `booking_id` references `bookings.id`

### `bookings`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `booking_code` | `VARCHAR(30)` | True | False | - |
| `customer_id` | `INTEGER` | True | False | - |
| `tour_id` | `INTEGER` | True | False | - |
| `tour_calendar_id` | `INTEGER` | True | False | - |
| `supplier_id` | `INTEGER` | True | False | - |
| `agent_id` | `INTEGER` | True | False | - |
| `affiliate_id` | `INTEGER` | True | False | - |
| `affiliate_ref_code` | `VARCHAR(60)` | True | False | - |
| `affiliate_attribution_id` | `INTEGER` | True | False | - |
| `created_by` | `INTEGER` | True | False | - |
| `booked_by_user_id` | `INTEGER` | True | False | - |
| `booking_source` | `VARCHAR(30)` | False | False | admin |
| `country_id` | `INTEGER` | True | False | - |
| `city_id` | `INTEGER` | True | False | - |
| `tour_name` | `VARCHAR(255)` | False | False |  |
| `tour_date` | `VARCHAR(30)` | False | False |  |
| `country` | `VARCHAR(100)` | False | False |  |
| `supplier_name` | `VARCHAR(150)` | False | False |  |
| `tour_start_date` | `DATETIME` | True | False | - |
| `tour_end_date` | `DATETIME` | True | False | - |
| `no_of_adults` | `INTEGER` | False | False | 1 |
| `no_of_children` | `INTEGER` | False | False | 0 |
| `no_of_infants` | `INTEGER` | False | False | 0 |
| `no_of_rooms` | `INTEGER` | True | False | - |
| `adults_count` | `INTEGER` | False | False | 1 |
| `children_count` | `INTEGER` | False | False | 0 |
| `total_travellers` | `INTEGER` | False | False | 1 |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `total_cost` | `NUMERIC(12, 2)` | False | False | 0 |
| `base_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `optional_activity_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `accommodation_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `extension_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `non_commissionable_addon_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `cost_plus_customer_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `cost_plus_supplier_payable` | `NUMERIC(12, 2)` | False | False | 0 |
| `discount_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `promo_code` | `VARCHAR(100)` | True | False | - |
| `group_discount_tier_id` | `INTEGER` | True | False | - |
| `group_discount_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `group_discount_funded_by` | `VARCHAR(20)` | True | False | - |
| `promo_discount_funded_by` | `VARCHAR(20)` | True | False | - |
| `tax_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `surcharge_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `service_fee_amount` | `NUMERIC(12, 2)` | True | False | - |
| `gateway_fee_amount` | `NUMERIC(12, 2)` | True | False | - |
| `final_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `agent_net_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `agent_markup` | `NUMERIC(12, 2)` | False | False | 0 |
| `customer_selling_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `amount_paid` | `NUMERIC(12, 2)` | False | False | 0 |
| `amount_pending` | `NUMERIC(12, 2)` | False | False | 0 |
| `price_source` | `VARCHAR(20)` | True | False | - |
| `date_price_id` | `INTEGER` | True | False | - |
| `adult_unit_price` | `NUMERIC(12, 2)` | True | False | - |
| `child_unit_price` | `NUMERIC(12, 2)` | True | False | - |
| `infant_unit_price` | `NUMERIC(12, 2)` | True | False | - |
| `single_supplement_amount` | `NUMERIC(12, 2)` | True | False | - |
| `group_discount_base_amount` | `NUMERIC(12, 2)` | True | False | - |
| `group_discount_percentage` | `NUMERIC(7, 4)` | True | False | - |
| `admin_markup_percentage` | `NUMERIC(5, 2)` | True | False | - |
| `supplier_base_amount` | `NUMERIC(12, 2)` | True | False | - |
| `admin_markup_amount` | `NUMERIC(12, 2)` | True | False | - |
| `commission_base_amount` | `NUMERIC(12, 2)` | True | False | - |
| `supplier_gross_amount` | `NUMERIC(12, 2)` | True | False | - |
| `supplier_discount_share_amount` | `NUMERIC(12, 2)` | True | False | - |
| `tourvaa_discount_share_amount` | `NUMERIC(12, 2)` | True | False | - |
| `tourvaa_gross_revenue` | `NUMERIC(12, 2)` | True | False | - |
| `agent_commission_base_amount` | `NUMERIC(12, 2)` | True | False | - |
| `affiliate_commission_base_amount` | `NUMERIC(12, 2)` | True | False | - |
| `financials_locked_at` | `DATETIME` | True | False | - |
| `tourvaa_commission_percentage` | `NUMERIC(5, 2)` | True | False | - |
| `tourvaa_commission_amount` | `NUMERIC(12, 2)` | True | False | - |
| `supplier_net_payable` | `NUMERIC(12, 2)` | True | False | - |
| `agent_commission_percentage` | `NUMERIC(5, 2)` | True | False | - |
| `agent_commission_amount` | `NUMERIC(12, 2)` | True | False | - |
| `affiliate_commission_percentage` | `NUMERIC(5, 2)` | True | False | - |
| `affiliate_commission_amount` | `NUMERIC(12, 2)` | True | False | - |
| `tourvaa_net_revenue` | `NUMERIC(12, 2)` | True | False | - |
| `pricing_slab_id` | `INTEGER` | True | False | - |
| `supplier_price` | `NUMERIC(12, 2)` | True | False | - |
| `supplier_currency` | `VARCHAR(10)` | True | False | - |
| `tourvaa_selling_price` | `NUMERIC(12, 2)` | True | False | - |
| `display_currency` | `VARCHAR(10)` | True | False | - |
| `exchange_rate` | `NUMERIC(14, 6)` | True | False | - |
| `exchange_rate_source` | `VARCHAR(30)` | True | False | - |
| `exchange_rate_captured_at` | `DATETIME` | True | False | - |
| `converted_customer_amount` | `NUMERIC(12, 2)` | True | False | - |
| `booking_status` | `VARCHAR(30)` | False | False | draft |
| `supplier_acceptance_status` | `VARCHAR(30)` | False | False | not_assigned |
| `payment_status` | `VARCHAR(30)` | False | False | unpaid |
| `payment_type` | `VARCHAR(30)` | False | False | full |
| `agent_payment_method` | `VARCHAR(30)` | True | False | - |
| `agent_reference` | `VARCHAR(100)` | True | False | - |
| `agent_hidden_at` | `DATETIME` | True | False | - |
| `notes` | `TEXT` | True | False | - |
| `customer_notes` | `TEXT` | True | False | - |
| `admin_notes` | `TEXT` | True | False | - |
| `cancellation_reason` | `VARCHAR(255)` | True | False | - |
| `cancellation_source` | `VARCHAR(30)` | True | False | - |
| `cancelled_at` | `DATETIME` | True | False | - |
| `cancelled_by` | `INTEGER` | True | False | - |
| `payment_due_date` | `DATETIME` | True | False | - |
| `cancellation_policy_snapshot` | `TEXT` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `affiliate_id` references `affiliates.id`
- Column `agent_id` references `agents.id`
- Column `supplier_id` references `suppliers.id`
- Column `tour_calendar_id` references `tour_calendar.id`
- Column `tour_id` references `tours.id`
- Column `cancelled_by` references `users.id`
- Column `pricing_slab_id` references `tour_pricing.id`
- Column `group_discount_tier_id` references `tour_group_discount_tiers.id`
- Column `city_id` references `cities.id`
- Column `country_id` references `countries.id`
- Column `booked_by_user_id` references `users.id`
- Column `created_by` references `users.id`
- Column `customer_id` references `customers.id`
- Column `affiliate_attribution_id` references `affiliate_attributions.id`

### `cancellation_requests`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `booking_id` | `INTEGER` | False | False | - |
| `customer_id` | `INTEGER` | False | False | - |
| `reason` | `TEXT` | False | False | - |
| `status` | `VARCHAR(30)` | False | False | pending |
| `refund_percentage` | `NUMERIC(5, 2)` | False | False | 0 |
| `refund_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `refund_processed_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `admin_notes` | `TEXT` | True | False | - |
| `reviewed_by` | `INTEGER` | True | False | - |
| `reviewed_at` | `DATETIME` | True | False | - |
| `gateway_refund_id` | `VARCHAR(150)` | True | False | - |
| `refund_processed_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `booking_id` references `bookings.id`
- Column `customer_id` references `customers.id`
- Column `reviewed_by` references `users.id`

### `chat_embeddings`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `source_type` | `VARCHAR(20)` | False | False | - |
| `source_id` | `INTEGER` | False | False | - |
| `content_text` | `TEXT` | False | False | - |
| `content_hash` | `VARCHAR(64)` | False | False | - |
| `embedding` | `JSON` | False | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `chat_faqs`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `question` | `VARCHAR(500)` | False | False | - |
| `answer` | `TEXT` | False | False | - |
| `category` | `VARCHAR(100)` | False | False | general |
| `sort_order` | `INTEGER` | False | False | 0 |
| `is_active` | `BOOLEAN` | False | False | True |
| `is_public` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `chat_feedback`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `message_id` | `INTEGER` | False | False | - |
| `session_id` | `INTEGER` | False | False | - |
| `rating` | `INTEGER` | False | False | - |
| `comment` | `TEXT` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `message_id` references `chat_messages.id`
- Column `session_id` references `chat_sessions.id`

### `chat_messages`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `session_id` | `INTEGER` | False | False | - |
| `role` | `VARCHAR(20)` | False | False | - |
| `content` | `TEXT` | False | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `session_id` references `chat_sessions.id`

### `chat_sessions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `session_key` | `VARCHAR(64)` | False | False | - |
| `user_name` | `VARCHAR(120)` | False | False |  |
| `user_email` | `VARCHAR(255)` | False | False |  |
| `created_at` | `DATETIME` | True | False | - |

### `checkout_sessions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `session_key` | `VARCHAR(64)` | False | False | - |
| `user_id` | `INTEGER` | True | False | - |
| `customer_id` | `INTEGER` | True | False | - |
| `tour_id` | `INTEGER` | True | False | - |
| `tour_calendar_id` | `INTEGER` | True | False | - |
| `step` | `VARCHAR(50)` | False | False | tour_selection |
| `status` | `VARCHAR(30)` | False | False | active |
| `data` | `JSON` | True | False | - |
| `booking_id` | `INTEGER` | True | False | - |
| `expires_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `customer_id` references `customers.id`
- Column `user_id` references `users.id`
- Column `tour_id` references `tours.id`
- Column `booking_id` references `bookings.id`
- Column `tour_calendar_id` references `tour_calendar.id`

### `cities`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `country_id` | `INTEGER` | False | False | - |
| `state_id` | `INTEGER` | True | False | - |
| `city_name` | `VARCHAR(120)` | False | False | - |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `state_id` references `states.id`
- Column `country_id` references `countries.id`

### `cms_blogs`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `title` | `VARCHAR(200)` | False | False | - |
| `slug` | `VARCHAR(220)` | False | False | - |
| `excerpt` | `TEXT` | True | False | - |
| `content` | `TEXT` | True | False | - |
| `featured_image` | `VARCHAR(255)` | True | False | - |
| `banner_title` | `VARCHAR(200)` | True | False | - |
| `banner_alt` | `VARCHAR(300)` | True | False | - |
| `author` | `VARCHAR(120)` | True | False | - |
| `tags` | `JSON` | True | False | - |
| `faqs` | `JSON` | True | False | - |
| `seo_title` | `VARCHAR(200)` | True | False | - |
| `seo_description` | `VARCHAR(400)` | True | False | - |
| `status` | `VARCHAR(20)` | False | False | draft |
| `published_at` | `DATETIME` | True | False | - |
| `scheduled_at` | `DATETIME` | True | False | - |
| `created_by` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `created_by` references `users.id`

### `cms_country_pages`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `country_id` | `INTEGER` | False | False | - |
| `hero_title` | `VARCHAR(200)` | True | False | - |
| `hero_description` | `TEXT` | True | False | - |
| `hero_image` | `VARCHAR(255)` | True | False | - |
| `showcase_title` | `VARCHAR(200)` | True | False | - |
| `showcase_description` | `TEXT` | True | False | - |
| `showcase_image` | `VARCHAR(255)` | True | False | - |
| `seo_title` | `VARCHAR(200)` | True | False | - |
| `seo_description` | `VARCHAR(400)` | True | False | - |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `country_id` references `countries.id`

### `cms_customer_reviews`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `reviewer_name` | `VARCHAR(120)` | False | False | - |
| `reviewer_image` | `VARCHAR(255)` | True | False | - |
| `rating` | `FLOAT` | False | False | 5 |
| `review_text` | `TEXT` | False | False | - |
| `tour_name` | `VARCHAR(200)` | True | False | - |
| `country` | `VARCHAR(100)` | True | False | - |
| `sort_order` | `INTEGER` | False | False | 0 |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `cms_external_links`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `label` | `VARCHAR(120)` | False | False | - |
| `url` | `VARCHAR(500)` | False | False | - |
| `open_in_new_tab` | `BOOLEAN` | False | False | True |
| `location` | `VARCHAR(50)` | False | False | footer |
| `sort_order` | `INTEGER` | False | False | 0 |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `cms_favourite_countries`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `country_id` | `INTEGER` | True | False | - |
| `title` | `VARCHAR(200)` | False | False | - |
| `snippet` | `TEXT` | True | False | - |
| `image` | `VARCHAR(255)` | True | False | - |
| `href` | `VARCHAR(500)` | True | False | - |
| `sort_order` | `INTEGER` | False | False | 0 |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `country_id` references `countries.id`

### `cms_footer_links`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `section_id` | `INTEGER` | False | False | - |
| `label` | `VARCHAR(120)` | False | False | - |
| `url` | `VARCHAR(500)` | False | False | - |
| `open_in_new_tab` | `BOOLEAN` | False | False | False |
| `sort_order` | `INTEGER` | False | False | 0 |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `section_id` references `cms_footer_sections.id`

### `cms_footer_sections`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `title` | `VARCHAR(120)` | False | False | - |
| `sort_order` | `INTEGER` | False | False | 0 |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `cms_handpicked_tours`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `sort_order` | `INTEGER` | False | False | 0 |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `cms_help_centre`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `category` | `VARCHAR(100)` | False | False | - |
| `question` | `TEXT` | False | False | - |
| `answer` | `TEXT` | False | False | - |
| `sort_order` | `INTEGER` | False | False | 0 |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `cms_homepage_banners`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `title` | `VARCHAR(200)` | False | False | - |
| `subtitle` | `VARCHAR(400)` | True | False | - |
| `image` | `VARCHAR(255)` | True | False | - |
| `video` | `VARCHAR(255)` | True | False | - |
| `cta_text` | `VARCHAR(100)` | True | False | - |
| `cta_url` | `VARCHAR(500)` | True | False | - |
| `sort_order` | `INTEGER` | False | False | 0 |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `cms_homepage_content_blocks`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `key` | `VARCHAR(60)` | False | False | - |
| `data` | `JSON` | False | False | <function dict at 0x000001A117F57ED0> |
| `version` | `INTEGER` | False | False | 1 |
| `updated_at` | `DATETIME` | True | False | - |

### `cms_pages`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `title` | `VARCHAR(200)` | False | False | - |
| `slug` | `VARCHAR(220)` | False | False | - |
| `content` | `TEXT` | True | False | - |
| `sections` | `JSON` | True | False | - |
| `seo_title` | `VARCHAR(200)` | True | False | - |
| `seo_description` | `VARCHAR(400)` | True | False | - |
| `status` | `VARCHAR(20)` | False | False | draft |
| `footer_section_id` | `INTEGER` | True | False | - |
| `sort_order` | `INTEGER` | False | False | 0 |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `footer_section_id` references `cms_footer_sections.id`

### `cms_policies`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `slug` | `VARCHAR(80)` | False | False | - |
| `title` | `VARCHAR(200)` | False | False | - |
| `content` | `TEXT` | False | False | - |
| `last_updated` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `cms_popular_destinations`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `country_id` | `INTEGER` | True | False | - |
| `city_id` | `INTEGER` | True | False | - |
| `title` | `VARCHAR(200)` | False | False | - |
| `image` | `VARCHAR(255)` | True | False | - |
| `description` | `TEXT` | True | False | - |
| `href` | `VARCHAR(500)` | True | False | - |
| `rating` | `FLOAT` | True | False | - |
| `package_count` | `INTEGER` | True | False | - |
| `sort_order` | `INTEGER` | False | False | 0 |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `country_id` references `countries.id`
- Column `city_id` references `cities.id`

### `cms_popular_tours`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `sort_order` | `INTEGER` | False | False | 0 |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `cms_promotional_popups`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `title` | `VARCHAR(200)` | False | False | - |
| `content` | `TEXT` | True | False | - |
| `image` | `VARCHAR(255)` | True | False | - |
| `cta_text` | `VARCHAR(100)` | True | False | - |
| `cta_url` | `VARCHAR(500)` | True | False | - |
| `display_after_seconds` | `INTEGER` | False | False | 3 |
| `display_frequency` | `VARCHAR(20)` | False | False | once |
| `is_active` | `BOOLEAN` | False | False | False |
| `valid_from` | `DATETIME` | True | False | - |
| `valid_until` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `cms_sitemap_entries`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `url` | `VARCHAR(500)` | False | False | - |
| `change_frequency` | `VARCHAR(20)` | False | False | weekly |
| `priority` | `VARCHAR(5)` | False | False | 0.5 |
| `last_modified` | `DATETIME` | True | False | - |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `cms_tours_on_deals`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `deal_label` | `VARCHAR(100)` | True | False | - |
| `discount_percentage` | `INTEGER` | False | False | 0 |
| `valid_until` | `DATETIME` | True | False | - |
| `sort_order` | `INTEGER` | False | False | 0 |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `contact_messages`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `name` | `VARCHAR(150)` | False | False | - |
| `email` | `VARCHAR(255)` | False | False | - |
| `phone` | `VARCHAR(30)` | True | False | - |
| `audience` | `VARCHAR(20)` | False | False | public |
| `enquiry_type` | `VARCHAR(50)` | False | False | General enquiry |
| `subject` | `VARCHAR(200)` | False | False | - |
| `message` | `TEXT` | False | False | - |
| `is_replied` | `BOOLEAN` | False | False | False |
| `created_at` | `DATETIME` | True | False | - |

### `conversations`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `participant_type` | `VARCHAR(20)` | False | False | - |
| `participant_user_id` | `INTEGER` | False | False | - |
| `status` | `VARCHAR(20)` | False | False | open |
| `last_message_at` | `DATETIME` | True | False | - |
| `last_message_preview` | `VARCHAR(300)` | True | False | - |
| `admin_unread_count` | `INTEGER` | False | False | 0 |
| `participant_unread_count` | `INTEGER` | False | False | 0 |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `participant_user_id` references `users.id`

### `countries`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `country_name` | `VARCHAR(120)` | False | False | - |
| `slug` | `VARCHAR(150)` | False | False | - |
| `country_code` | `VARCHAR(10)` | False | False | - |
| `phone_code` | `VARCHAR(10)` | False | False |  |
| `currency_code` | `VARCHAR(10)` | False | False |  |
| `flag_emoji` | `VARCHAR(16)` | False | False |  |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `currencies`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `name` | `VARCHAR(120)` | False | False | - |
| `code` | `VARCHAR(10)` | False | False | - |
| `symbol` | `VARCHAR(10)` | False | False | - |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `customer_cancellation_requests`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `customer_id` | `INTEGER` | False | False | - |
| `booking_id` | `INTEGER` | False | False | - |
| `reason` | `TEXT` | False | False | - |
| `status` | `VARCHAR(30)` | False | False | requested |
| `admin_notes` | `TEXT` | True | False | - |
| `reviewed_by` | `INTEGER` | True | False | - |
| `reviewed_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `reviewed_by` references `users.id`
- Column `booking_id` references `bookings.id`
- Column `customer_id` references `customers.id`

### `customer_communications`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `customer_id` | `INTEGER` | True | False | - |
| `booking_id` | `INTEGER` | True | False | - |
| `subject` | `VARCHAR(150)` | False | False | - |
| `message` | `TEXT` | False | False | - |
| `sent_by_user_id` | `INTEGER` | True | False | - |
| `sent_to_email` | `VARCHAR(150)` | False | False | admin |
| `message_type` | `VARCHAR(30)` | False | False | admin_message |
| `email_status` | `VARCHAR(20)` | False | False | pending |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `sent_by_user_id` references `users.id`
- Column `customer_id` references `customers.id`
- Column `booking_id` references `bookings.id`

### `customer_saved_travellers`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `customer_id` | `INTEGER` | False | False | - |
| `traveller_name` | `VARCHAR(150)` | False | False | - |
| `email` | `VARCHAR(150)` | False | False |  |
| `phone` | `VARCHAR(50)` | False | False |  |
| `traveller_type` | `VARCHAR(20)` | False | False | adult |
| `age` | `INTEGER` | True | False | - |
| `gender` | `VARCHAR(30)` | True | False | - |
| `passport_number` | `VARCHAR(100)` | True | False | - |
| `allergies` | `TEXT` | True | False | - |
| `special_notes` | `TEXT` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `customer_id` references `customers.id`

### `customer_wishlist_items`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `user_id` | `INTEGER` | False | False | - |
| `tour_id` | `INTEGER` | False | False | - |
| `created_at` | `DATETIME` | False | False | - |
| `last_reminder_sent_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`
- Column `user_id` references `users.id`

### `customers`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `user_id` | `INTEGER` | True | False | - |
| `customer_code` | `VARCHAR(30)` | True | False | - |
| `customer_type` | `VARCHAR(20)` | False | False | registered |
| `agent_id` | `INTEGER` | True | False | - |
| `first_name` | `VARCHAR(75)` | False | False |  |
| `last_name` | `VARCHAR(75)` | False | False |  |
| `full_name` | `VARCHAR(150)` | False | False | - |
| `email` | `VARCHAR(150)` | False | False | - |
| `phone_country_code` | `VARCHAR(10)` | False | False |  |
| `phone` | `VARCHAR(30)` | False | False |  |
| `country_id` | `INTEGER` | True | False | - |
| `city_id` | `INTEGER` | True | False | - |
| `date_of_birth` | `DATETIME` | True | False | - |
| `gender` | `VARCHAR(30)` | True | False | - |
| `nationality` | `VARCHAR(100)` | False | False |  |
| `passport_number` | `VARCHAR(100)` | False | False |  |
| `passport_expiry` | `VARCHAR(40)` | False | False |  |
| `frequent_flyer` | `VARCHAR(100)` | False | False |  |
| `preferred_airline` | `VARCHAR(100)` | False | False |  |
| `emergency_name` | `VARCHAR(150)` | False | False |  |
| `emergency_relation` | `VARCHAR(100)` | False | False |  |
| `emergency_phone` | `VARCHAR(30)` | False | False |  |
| `emergency_email` | `VARCHAR(150)` | False | False |  |
| `address_line_1` | `VARCHAR(255)` | False | False |  |
| `address_line_2` | `VARCHAR(255)` | False | False |  |
| `postal_code` | `VARCHAR(20)` | False | False |  |
| `address` | `VARCHAR(255)` | False | False |  |
| `profile_image` | `VARCHAR(255)` | False | False |  |
| `country` | `VARCHAR(100)` | False | False |  |
| `state` | `VARCHAR(100)` | False | False |  |
| `city` | `VARCHAR(100)` | False | False |  |
| `pincode` | `VARCHAR(20)` | False | False |  |
| `status` | `VARCHAR(20)` | False | False | active |
| `email_verified` | `BOOLEAN` | False | False | False |
| `phone_verified` | `BOOLEAN` | False | False | False |
| `is_blocked` | `BOOLEAN` | False | False | False |
| `blocked_reason` | `VARCHAR(255)` | True | False | - |
| `blocked_at` | `DATETIME` | True | False | - |
| `blocked_by` | `INTEGER` | True | False | - |
| `total_bookings` | `INTEGER` | False | False | 0 |
| `completed_bookings` | `INTEGER` | False | False | 0 |
| `cancelled_bookings` | `INTEGER` | False | False | 0 |
| `upcoming_bookings` | `INTEGER` | False | False | 0 |
| `total_amount_paid` | `NUMERIC(12, 2)` | False | False | 0 |
| `total_amount_pending` | `NUMERIC(12, 2)` | False | False | 0 |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `user_id` references `users.id`
- Column `city_id` references `cities.id`
- Column `blocked_by` references `users.id`
- Column `country_id` references `countries.id`
- Column `agent_id` references `agents.id`

### `email_logs`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `recipient_email` | `VARCHAR(180)` | False | False | - |
| `subject` | `VARCHAR(255)` | False | False | - |
| `template_key` | `VARCHAR(100)` | True | False | - |
| `entity_type` | `VARCHAR(60)` | True | False | - |
| `entity_id` | `INTEGER` | True | False | - |
| `status` | `VARCHAR(30)` | False | False | pending |
| `error_message` | `TEXT` | True | False | - |
| `sent_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |

### `email_templates`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `key` | `VARCHAR(100)` | False | False | - |
| `name` | `VARCHAR(150)` | False | False | - |
| `subject` | `VARCHAR(200)` | False | False | - |
| `body` | `TEXT` | False | False | - |
| `is_active` | `BOOLEAN` | True | False | True |
| `updated_at` | `DATETIME` | True | False | - |

### `external_affiliate_clicks`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `provider` | `VARCHAR(40)` | False | False | - |
| `product_code` | `VARCHAR(80)` | False | False | - |
| `product_title` | `VARCHAR(255)` | True | False | - |
| `provider_destination_id` | `VARCHAR(40)` | True | False | - |
| `tourvaa_country_id` | `INTEGER` | True | False | - |
| `tourvaa_city_id` | `INTEGER` | True | False | - |
| `user_id` | `INTEGER` | True | False | - |
| `agent_id` | `INTEGER` | True | False | - |
| `session_id` | `VARCHAR(64)` | True | False | - |
| `campaign` | `VARCHAR(80)` | True | False | - |
| `source_page` | `VARCHAR(40)` | True | False | - |
| `page_path` | `VARCHAR(255)` | True | False | - |
| `external_url` | `TEXT` | True | False | - |
| `external_url_hash` | `VARCHAR(64)` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tourvaa_country_id` references `countries.id`
- Column `agent_id` references `agents.id`
- Column `tourvaa_city_id` references `cities.id`
- Column `user_id` references `users.id`

### `external_destination_mappings`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `provider` | `VARCHAR(40)` | False | False | - |
| `provider_destination_id` | `VARCHAR(40)` | False | False | - |
| `provider_destination_name` | `VARCHAR(255)` | False | False | - |
| `provider_destination_type` | `VARCHAR(40)` | True | False | - |
| `provider_parent_destination_id` | `VARCHAR(40)` | True | False | - |
| `provider_default_currency` | `VARCHAR(3)` | True | False | - |
| `provider_destination_url` | `TEXT` | True | False | - |
| `slug` | `VARCHAR(191)` | False | False | - |
| `tourvaa_country_id` | `INTEGER` | True | False | - |
| `tourvaa_state_id` | `INTEGER` | True | False | - |
| `tourvaa_city_id` | `INTEGER` | True | False | - |
| `mapping_source` | `VARCHAR(10)` | True | False | - |
| `is_active` | `BOOLEAN` | False | False | True |
| `last_synced_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tourvaa_city_id` references `cities.id`
- Column `tourvaa_state_id` references `states.id`
- Column `tourvaa_country_id` references `countries.id`

### `external_providers`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `code` | `VARCHAR(40)` | False | False | - |
| `name` | `VARCHAR(100)` | False | False | - |
| `public_category` | `VARCHAR(120)` | False | False | Day Tours & Experiences |
| `show_on_homepage` | `BOOLEAN` | False | False | True |
| `show_on_destination_pages` | `BOOLEAN` | False | False | True |
| `show_on_itinerary` | `BOOLEAN` | False | False | True |
| `show_in_search` | `BOOLEAN` | False | False | True |
| `last_connection_status` | `VARCHAR(20)` | True | False | - |
| `last_connection_message` | `VARCHAR(255)` | True | False | - |
| `last_connection_at` | `DATETIME` | True | False | - |
| `last_destination_sync_at` | `DATETIME` | True | False | - |
| `last_destination_sync_status` | `VARCHAR(20)` | True | False | - |
| `last_destination_sync_count` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `invoice_items`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `invoice_id` | `INTEGER` | False | False | - |
| `item_type` | `VARCHAR(40)` | False | False | booking |
| `description` | `VARCHAR(255)` | False | False | - |
| `quantity` | `INTEGER` | False | False | 1 |
| `unit_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `tax_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `total_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `invoice_id` references `invoices.id`

### `invoices`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `invoice_number` | `VARCHAR(40)` | True | False | - |
| `booking_id` | `INTEGER` | False | False | - |
| `payment_id` | `INTEGER` | True | False | - |
| `customer_id` | `INTEGER` | True | False | - |
| `invoice_type` | `VARCHAR(30)` | False | False | tax_invoice |
| `recipient_type` | `VARCHAR(20)` | False | False | customer |
| `document_snapshot` | `JSON` | True | False | - |
| `status` | `VARCHAR(30)` | False | False | generated |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `subtotal_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `gst_rate` | `NUMERIC(5, 4)` | False | False | 0.18 |
| `gst_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `total_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `amount_paid` | `NUMERIC(12, 2)` | False | False | 0 |
| `amount_due` | `NUMERIC(12, 2)` | False | False | 0 |
| `balance_due_date` | `DATETIME` | True | False | - |
| `balance_reminder_stage` | `VARCHAR(20)` | True | False | - |
| `last_balance_reminder_at` | `DATETIME` | True | False | - |
| `pdf_path` | `VARCHAR(255)` | True | False | - |
| `emailed_at` | `DATETIME` | True | False | - |
| `created_by` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `booking_id` references `bookings.id`
- Column `payment_id` references `payments.id`
- Column `created_by` references `users.id`
- Column `customer_id` references `customers.id`

### `login_history`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `user_id` | `INTEGER` | True | False | - |
| `email` | `VARCHAR(150)` | False | False | - |
| `status` | `VARCHAR(30)` | False | False | - |
| `failure_reason` | `VARCHAR(255)` | True | False | - |
| `client_type` | `VARCHAR(30)` | False | False | web |
| `device_id` | `VARCHAR(120)` | True | False | - |
| `device_name` | `VARCHAR(180)` | True | False | - |
| `ip_address` | `VARCHAR(100)` | True | False | - |
| `user_agent` | `VARCHAR(255)` | True | False | - |
| `session_id` | `VARCHAR(120)` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `user_id` references `users.id`

### `message_replies`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `communication_id` | `INTEGER` | False | False | - |
| `sender_user_id` | `INTEGER` | True | False | - |
| `sender_type` | `VARCHAR(30)` | False | False | admin |
| `message` | `TEXT` | False | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `sender_user_id` references `users.id`
- Column `communication_id` references `booking_communications.id`

### `messages`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `conversation_id` | `INTEGER` | False | False | - |
| `sender_user_id` | `INTEGER` | True | False | - |
| `sender_role` | `VARCHAR(20)` | False | False | - |
| `body` | `TEXT` | False | False | - |
| `is_deleted` | `BOOLEAN` | False | False | False |
| `deleted_at` | `DATETIME` | True | False | - |
| `delivered_at` | `DATETIME` | True | False | - |
| `read_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `sender_user_id` references `users.id`
- Column `conversation_id` references `conversations.id`

### `newsletter_subscribers`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `email` | `VARCHAR(255)` | False | False | - |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |

### `notification_deliveries`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `event_type` | `VARCHAR(100)` | False | False | - |
| `entity_type` | `VARCHAR(60)` | False | False | - |
| `entity_id` | `INTEGER` | False | False | - |
| `recipient_type` | `VARCHAR(40)` | False | False | - |
| `recipient_email` | `VARCHAR(180)` | False | False | - |
| `template_key` | `VARCHAR(100)` | False | False | - |
| `subject` | `VARCHAR(255)` | True | False | - |
| `payload_json` | `JSON` | True | False | - |
| `status` | `VARCHAR(30)` | False | False | pending |
| `attempt_count` | `INTEGER` | False | False | 0 |
| `next_attempt_at` | `DATETIME` | True | False | - |
| `lease_token` | `VARCHAR(64)` | True | False | - |
| `lease_expires_at` | `DATETIME` | True | False | - |
| `error_message` | `TEXT` | True | False | - |
| `idempotency_key` | `VARCHAR(255)` | False | False | - |
| `sent_at` | `DATETIME` | True | False | - |
| `smtp_accepted_at` | `DATETIME` | True | False | - |
| `exhausted_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `notification_logs`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `notification_id` | `INTEGER` | True | False | - |
| `channel` | `VARCHAR(30)` | False | False | - |
| `status` | `VARCHAR(30)` | False | False | - |
| `response` | `TEXT` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `notification_id` references `notifications.id`

### `notifications`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `user_id` | `INTEGER` | True | False | - |
| `notification_type` | `VARCHAR(60)` | False | False | - |
| `title` | `VARCHAR(180)` | False | False | - |
| `message` | `TEXT` | False | False | - |
| `channel` | `VARCHAR(30)` | False | False | in_app |
| `status` | `VARCHAR(30)` | False | False | pending |
| `is_read` | `INTEGER` | False | False | 0 |
| `entity_type` | `VARCHAR(60)` | True | False | - |
| `entity_id` | `INTEGER` | True | False | - |
| `notification_id` | `VARCHAR(100)` | True | False | - |
| `metadata_json` | `JSON` | True | False | - |
| `event_key` | `VARCHAR(100)` | True | False | - |
| `event_version` | `VARCHAR(100)` | True | False | - |
| `idempotency_key` | `VARCHAR(255)` | True | False | - |
| `sent_at` | `DATETIME` | True | False | - |
| `read_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `user_id` references `users.id`

### `payment_holds`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `payment_id` | `INTEGER` | False | False | - |
| `booking_id` | `INTEGER` | False | False | - |
| `hold_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `captured_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `released_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `status` | `VARCHAR(30)` | False | False | active |
| `expires_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `payment_id` references `payments.id`
- Column `booking_id` references `bookings.id`

### `payment_settings`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `provider_name` | `VARCHAR(100)` | False | False | - |
| `is_enabled` | `BOOLEAN` | False | False | False |
| `public_key` | `TEXT` | True | False | - |
| `secret_key` | `TEXT` | True | False | - |
| `webhook_id` | `VARCHAR(150)` | True | False | - |
| `sandbox_client_id` | `TEXT` | True | False | - |
| `sandbox_secret` | `TEXT` | True | False | - |
| `live_client_id` | `TEXT` | True | False | - |
| `live_secret` | `TEXT` | True | False | - |
| `surcharge_percentage` | `VARCHAR(20)` | False | False | 0 |
| `mode` | `VARCHAR(20)` | False | False | test |
| `last_test_status` | `VARCHAR(20)` | True | False | - |
| `last_test_at` | `DATETIME` | True | False | - |
| `last_test_error` | `TEXT` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `payment_transactions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `payment_id` | `INTEGER` | False | False | - |
| `booking_id` | `INTEGER` | False | False | - |
| `transaction_type` | `VARCHAR(30)` | False | False | - |
| `amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `status` | `VARCHAR(30)` | False | False | success |
| `gateway_reference` | `VARCHAR(150)` | True | False | - |
| `metadata_json` | `JSON` | True | False | - |
| `created_by` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `booking_id` references `bookings.id`
- Column `payment_id` references `payments.id`
- Column `created_by` references `users.id`

### `payments`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `payment_code` | `VARCHAR(30)` | True | False | - |
| `booking_id` | `INTEGER` | False | False | - |
| `customer_id` | `INTEGER` | True | False | - |
| `created_by` | `INTEGER` | True | False | - |
| `payment_method` | `VARCHAR(30)` | False | False | card |
| `payment_type` | `VARCHAR(30)` | False | False | full |
| `gateway` | `VARCHAR(50)` | False | False | manual |
| `gateway_payment_id` | `VARCHAR(150)` | True | False | - |
| `gateway_order_id` | `VARCHAR(150)` | True | False | - |
| `idempotency_key` | `VARCHAR(150)` | True | False | - |
| `total_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `authorized_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `captured_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `paid_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `pending_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `gst_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `surcharge_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `refunded_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `payment_status` | `VARCHAR(30)` | False | False | pending |
| `transaction_id` | `VARCHAR(100)` | True | False | - |
| `payment_date` | `VARCHAR(30)` | True | False | - |
| `notes` | `TEXT` | True | False | - |
| `failure_reason` | `VARCHAR(255)` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `customer_id` references `customers.id`
- Column `created_by` references `users.id`
- Column `booking_id` references `bookings.id`

### `permissions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `name` | `VARCHAR(150)` | False | False | - |
| `slug` | `VARCHAR(150)` | False | False | - |
| `module` | `VARCHAR(100)` | False | False | - |
| `action` | `VARCHAR(20)` | False | False | get |
| `is_active` | `BOOLEAN` | True | False | True |
| `is_system` | `BOOLEAN` | False | False | False |
| `created_at` | `DATETIME` | True | False | - |

### `push_delivery_logs`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `notification_id` | `INTEGER` | True | False | - |
| `subscription_id` | `INTEGER` | True | False | - |
| `event_key` | `VARCHAR(100)` | True | False | - |
| `recipient_user_id` | `INTEGER` | True | False | - |
| `provider` | `VARCHAR(30)` | False | False | web_push |
| `status` | `VARCHAR(30)` | False | False | pending |
| `attempt_count` | `INTEGER` | False | False | 0 |
| `error_message` | `TEXT` | True | False | - |
| `sent_at` | `DATETIME` | True | False | - |
| `failed_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `recipient_user_id` references `users.id`
- Column `notification_id` references `notifications.id`
- Column `subscription_id` references `push_subscriptions.id`

### `push_subscriptions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `user_id` | `INTEGER` | True | False | - |
| `endpoint` | `TEXT` | False | False | - |
| `endpoint_hash` | `VARCHAR(64)` | False | False | - |
| `p256dh` | `VARCHAR(256)` | False | False | - |
| `auth` | `VARCHAR(255)` | False | False | - |
| `platform` | `VARCHAR(20)` | True | False | - |
| `device_type` | `VARCHAR(30)` | True | False | - |
| `is_active` | `INTEGER` | False | False | 1 |
| `last_used_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `user_id` references `users.id`

### `refund_rules`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | True | False | - |
| `days_before_tour_min` | `INTEGER` | False | False | - |
| `days_before_tour_max` | `INTEGER` | True | False | - |
| `refund_percentage` | `NUMERIC(5, 2)` | False | False | 0 |
| `description` | `VARCHAR(255)` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `report_schedules`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `report_type` | `VARCHAR(50)` | False | False | - |
| `cadence` | `VARCHAR(20)` | False | False | weekly |
| `recipient_emails` | `VARCHAR(1000)` | False | False | - |
| `is_active` | `BOOLEAN` | False | False | True |
| `created_by` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `last_run_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `created_by` references `users.id`

### `role_permissions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `role_id` | `INTEGER` | False | False | - |
| `permission_id` | `INTEGER` | False | False | - |

**Foreign Keys:**
- Column `permission_id` references `permissions.id`
- Column `role_id` references `roles.id`

### `roles`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `name` | `VARCHAR(100)` | False | False | - |
| `slug` | `VARCHAR(100)` | False | False | - |
| `is_active` | `BOOLEAN` | True | False | True |
| `is_system` | `BOOLEAN` | False | False | False |
| `created_at` | `DATETIME` | True | False | - |

### `smtp_settings`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `is_enabled` | `BOOLEAN` | False | False | False |
| `host` | `VARCHAR(255)` | True | False | - |
| `port` | `INTEGER` | False | False | 465 |
| `username` | `VARCHAR(255)` | True | False | - |
| `password` | `TEXT` | True | False | - |
| `from_name` | `VARCHAR(150)` | False | False | Tourvaa |
| `from_email` | `VARCHAR(255)` | True | False | - |
| `reply_to` | `VARCHAR(255)` | True | False | - |
| `admin_notification_to` | `TEXT` | True | False | - |
| `admin_notification_cc` | `TEXT` | True | False | - |
| `admin_notification_bcc` | `TEXT` | True | False | - |
| `use_ssl` | `BOOLEAN` | False | False | True |
| `use_starttls` | `BOOLEAN` | False | False | False |
| `timeout_seconds` | `INTEGER` | False | False | 20 |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `states`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `country_id` | `INTEGER` | False | False | - |
| `state_name` | `VARCHAR(150)` | False | False | - |
| `state_code` | `VARCHAR(10)` | False | False |  |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `country_id` references `countries.id`

### `supplier_approval_history`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `supplier_id` | `INTEGER` | False | False | - |
| `from_status` | `VARCHAR(30)` | True | False | - |
| `to_status` | `VARCHAR(30)` | False | False | - |
| `notes` | `TEXT` | True | False | - |
| `changed_by` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | False | False | - |

**Foreign Keys:**
- Column `supplier_id` references `suppliers.id`
- Column `changed_by` references `users.id`

### `supplier_business_info`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `supplier_id` | `INTEGER` | False | False | - |
| `years_in_business` | `INTEGER` | False | False | 0 |
| `certificate_of_incorporation` | `VARCHAR(255)` | False | False |  |
| `monthly_customers_count` | `INTEGER` | False | False | 0 |
| `target_market` | `VARCHAR(255)` | False | False |  |
| `destinations_sold` | `TEXT` | False | False |  |
| `gst_tax_number` | `VARCHAR(100)` | False | False |  |
| `business_registration_number` | `VARCHAR(100)` | False | False |  |
| `trading_name` | `VARCHAR(150)` | False | False |  |
| `business_email` | `VARCHAR(150)` | False | False |  |
| `website_url` | `VARCHAR(255)` | False | False |  |
| `approval_status` | `VARCHAR(30)` | False | False | pending |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `supplier_id` references `suppliers.id`

### `supplier_contacts`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `supplier_id` | `INTEGER` | False | False | - |
| `contact_name` | `VARCHAR(150)` | False | False | - |
| `first_name` | `VARCHAR(75)` | False | False |  |
| `last_name` | `VARCHAR(75)` | False | False |  |
| `designation` | `VARCHAR(100)` | False | False |  |
| `phone` | `VARCHAR(30)` | False | False |  |
| `email` | `VARCHAR(150)` | False | False |  |
| `alternate_phone` | `VARCHAR(30)` | False | False |  |
| `preferred_contact_method` | `VARCHAR(20)` | False | False |  |
| `is_primary` | `BOOLEAN` | False | False | False |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `supplier_id` references `suppliers.id`

### `supplier_documents`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `supplier_id` | `INTEGER` | False | False | - |
| `document_type` | `VARCHAR(100)` | False | False | - |
| `document_name` | `VARCHAR(150)` | False | False | - |
| `file_path` | `VARCHAR(255)` | False | False | - |
| `file_size` | `INTEGER` | False | False | 0 |
| `mime_type` | `VARCHAR(100)` | False | False |  |
| `status` | `VARCHAR(20)` | False | False | pending |
| `rejection_reason` | `VARCHAR(255)` | True | False | - |
| `uploaded_at` | `DATETIME` | True | False | - |
| `reviewed_at` | `DATETIME` | True | False | - |
| `reviewed_by` | `INTEGER` | True | False | - |

**Foreign Keys:**
- Column `supplier_id` references `suppliers.id`
- Column `reviewed_by` references `users.id`

### `supplier_invoicing`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `supplier_id` | `INTEGER` | False | False | - |
| `contact_name` | `VARCHAR(150)` | False | False |  |
| `email` | `VARCHAR(150)` | False | False |  |
| `phone` | `VARCHAR(30)` | False | False |  |
| `preferred_payment_method` | `VARCHAR(30)` | False | False |  |
| `account_name` | `VARCHAR(150)` | False | False |  |
| `account_number` | `VARCHAR(100)` | False | False |  |
| `bank_name` | `VARCHAR(150)` | False | False |  |
| `bank_branch` | `VARCHAR(150)` | False | False |  |
| `swift_code` | `VARCHAR(50)` | False | False |  |
| `iban` | `VARCHAR(100)` | False | False |  |
| `bank_country_id` | `INTEGER` | True | False | - |
| `country_id` | `INTEGER` | True | False | - |
| `tax_number` | `VARCHAR(100)` | False | False |  |
| `billing_address` | `TEXT` | True | False | - |
| `billing_city` | `VARCHAR(100)` | False | False |  |
| `billing_state` | `VARCHAR(100)` | False | False |  |
| `billing_postal_code` | `VARCHAR(30)` | False | False |  |
| `bank_edit_requested_at` | `DATETIME` | True | False | - |
| `bank_edit_unlocked_at` | `DATETIME` | True | False | - |
| `bank_edit_unlocked_by` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `supplier_id` references `suppliers.id`
- Column `bank_edit_unlocked_by` references `users.id`
- Column `bank_country_id` references `countries.id`
- Column `country_id` references `countries.id`

### `supplier_ledgers`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `supplier_id` | `INTEGER` | False | False | - |
| `booking_id` | `INTEGER` | False | False | - |
| `gross_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `commission_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `commission_percentage` | `NUMERIC(5, 2)` | False | False | 0 |
| `net_payable` | `NUMERIC(12, 2)` | False | False | 0 |
| `amount_paid` | `NUMERIC(12, 2)` | False | False | 0 |
| `amount_pending` | `NUMERIC(12, 2)` | False | False | 0 |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `status` | `VARCHAR(30)` | False | False | pending |
| `notes` | `TEXT` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `supplier_id` references `suppliers.id`
- Column `booking_id` references `bookings.id`

### `supplier_payout_items`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `payout_id` | `INTEGER` | False | False | - |
| `ledger_id` | `INTEGER` | False | False | - |
| `amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `payout_id` references `supplier_payouts.id`
- Column `ledger_id` references `supplier_ledgers.id`

### `supplier_payouts`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `payout_code` | `VARCHAR(30)` | True | False | - |
| `supplier_id` | `INTEGER` | False | False | - |
| `total_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `payment_method` | `VARCHAR(50)` | False | False | bank_transfer |
| `reference_number` | `VARCHAR(150)` | True | False | - |
| `status` | `VARCHAR(30)` | False | False | pending |
| `notes` | `TEXT` | True | False | - |
| `initiated_by` | `INTEGER` | True | False | - |
| `approved_by` | `INTEGER` | True | False | - |
| `paid_by` | `INTEGER` | True | False | - |
| `paid_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `paid_by` references `users.id`
- Column `initiated_by` references `users.id`
- Column `approved_by` references `users.id`
- Column `supplier_id` references `suppliers.id`

### `supplier_vehicles`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `supplier_id` | `INTEGER` | False | False | - |
| `make` | `VARCHAR(100)` | False | False |  |
| `model` | `VARCHAR(100)` | False | False |  |
| `vehicle_type` | `VARCHAR(75)` | False | False |  |
| `registration_number` | `VARCHAR(100)` | False | False |  |
| `year` | `INTEGER` | True | False | - |
| `capacity` | `INTEGER` | True | False | - |
| `fitness_certificate` | `VARCHAR(255)` | False | False |  |
| `insurance_document` | `VARCHAR(255)` | False | False |  |
| `vehicle_photos` | `TEXT` | False | False |  |
| `approval_status` | `VARCHAR(30)` | False | False | pending |
| `rejection_reason` | `VARCHAR(255)` | True | False | - |
| `reviewed_at` | `DATETIME` | True | False | - |
| `reviewed_by` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `reviewed_by` references `users.id`
- Column `supplier_id` references `suppliers.id`

### `suppliers`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `user_id` | `INTEGER` | True | False | - |
| `supplier_code` | `VARCHAR(30)` | True | False | - |
| `supplier_name` | `VARCHAR(150)` | False | False | - |
| `supplier_type` | `VARCHAR(75)` | False | False |  |
| `country_id` | `INTEGER` | True | False | - |
| `city_id` | `INTEGER` | True | False | - |
| `currency` | `VARCHAR(10)` | True | False | - |
| `years_in_operation` | `INTEGER` | False | False | 0 |
| `status` | `VARCHAR(20)` | False | False | inactive |
| `approval_status` | `VARCHAR(30)` | False | False | pending |
| `rejection_reason` | `VARCHAR(255)` | True | False | - |
| `admin_comments` | `TEXT` | True | False | - |
| `pending_requirements` | `TEXT` | True | False | - |
| `approved_at` | `DATETIME` | True | False | - |
| `approved_by` | `INTEGER` | True | False | - |
| `rejected_at` | `DATETIME` | True | False | - |
| `rejected_by` | `INTEGER` | True | False | - |
| `commission_percentage` | `NUMERIC(5, 2)` | True | False | - |
| `onboarding_completed_at` | `DATETIME` | True | False | - |
| `commission_accepted_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `rejected_by` references `users.id`
- Column `approved_by` references `users.id`
- Column `city_id` references `cities.id`
- Column `country_id` references `countries.id`
- Column `user_id` references `users.id`

### `tour_accommodation_extras`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `accommodation_name` | `VARCHAR(255)` | False | False | - |
| `description` | `TEXT` | True | False |  |
| `extra_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `price_type` | `VARCHAR(20)` | False | False | per_person |
| `image` | `VARCHAR(255)` | True | False |  |
| `category` | `VARCHAR(30)` | False | False | room_upgrade |
| `is_default` | `INTEGER` | False | False | 0 |
| `status` | `VARCHAR(20)` | False | False | active |
| `commissionable` | `BOOLEAN` | False | False | True |
| `supplier_cost` | `NUMERIC(12, 2)` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_availability_configs`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `availability_start_date` | `DATETIME` | True | False | - |
| `availability_end_date` | `DATETIME` | True | False | - |
| `min_advance_booking_days` | `INTEGER` | False | False | 0 |
| `agent_no_deposit_buffer_weeks` | `INTEGER` | False | False | 4 |
| `agent_reserve_deposit_percentage` | `FLOAT` | False | False | 30.0 |
| `frequency` | `VARCHAR(20)` | True | False | - |
| `frequency_week` | `INTEGER` | True | False | - |
| `frequency_weeks` | `JSON` | True | False | - |
| `frequency_days` | `JSON` | True | False | - |
| `seats_per_occurrence` | `INTEGER` | False | False | 0 |
| `last_end_date_reminder_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_calendar`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `tour_date` | `DATETIME` | False | False | - |
| `tour_date_day` | `DATE` | False | False | - |
| `start_date` | `DATETIME` | True | False | - |
| `end_date` | `DATETIME` | True | False | - |
| `available_seats` | `INTEGER` | False | False | 0 |
| `booked_seats` | `INTEGER` | False | False | 0 |
| `status` | `VARCHAR(20)` | False | False | available |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_categories`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `category_name` | `VARCHAR(120)` | False | False | - |
| `slug` | `VARCHAR(150)` | False | False | - |
| `description` | `TEXT` | False | False |  |
| `image` | `VARCHAR(255)` | False | False |  |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

### `tour_date_prices`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `price_date` | `DATE` | False | False | - |
| `adult_price` | `NUMERIC(12, 2)` | False | False | - |
| `child_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_discount_history`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `discount_id` | `INTEGER` | False | False | - |
| `version_number` | `INTEGER` | False | False | - |
| `change_type` | `VARCHAR(30)` | False | False | - |
| `discount_name` | `VARCHAR(255)` | False | False | - |
| `discount_type` | `VARCHAR(20)` | False | False | - |
| `discount_value` | `NUMERIC(12, 2)` | False | False | - |
| `start_date` | `DATETIME` | True | False | - |
| `end_date` | `DATETIME` | True | False | - |
| `reason` | `VARCHAR(500)` | True | False | - |
| `changed_by` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `changed_by` references `users.id`
- Column `discount_id` references `tour_discounts.id`

### `tour_discount_redemptions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `discount_id` | `INTEGER` | False | False | - |
| `booking_id` | `INTEGER` | False | False | - |
| `discount_amount` | `NUMERIC(12, 2)` | False | False | - |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `applied_at` | `DATETIME` | False | False | - |

**Foreign Keys:**
- Column `discount_id` references `tour_discounts.id`
- Column `booking_id` references `bookings.id`

### `tour_discounts`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | True | False | - |
| `category_id` | `INTEGER` | True | False | - |
| `country_id` | `INTEGER` | True | False | - |
| `discount_name` | `VARCHAR(255)` | False | False | - |
| `discount_code` | `VARCHAR(50)` | True | False | - |
| `discount_type` | `VARCHAR(20)` | False | False | - |
| `discount_value` | `NUMERIC(12, 2)` | False | False | - |
| `discount_scope` | `VARCHAR(20)` | False | False | tour |
| `start_date` | `DATETIME` | True | False | - |
| `end_date` | `DATETIME` | True | False | - |
| `usage_limit` | `INTEGER` | True | False | - |
| `used_count` | `INTEGER` | False | False | 0 |
| `minimum_booking_amount` | `NUMERIC(12, 2)` | False | False | 0 |
| `status` | `VARCHAR(20)` | False | False | active |
| `funded_by` | `VARCHAR(20)` | False | False | SUPPLIER |
| `show_on_website` | `BOOLEAN` | False | False | True |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`
- Column `country_id` references `countries.id`
- Column `category_id` references `tour_categories.id`

### `tour_exclusions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `icon` | `VARCHAR(255)` | False | False |  |
| `title` | `VARCHAR(255)` | False | False | - |
| `description` | `TEXT` | True | False |  |
| `display_order` | `INTEGER` | False | False | 0 |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_extensions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `extension_tour_id` | `INTEGER` | False | False | - |
| `extension_title` | `VARCHAR(255)` | False | False |  |
| `extension_note` | `TEXT` | True | False |  |
| `extra_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `price_type` | `VARCHAR(20)` | False | False | per_booking |
| `category` | `VARCHAR(30)` | False | False | other |
| `display_order` | `INTEGER` | False | False | 0 |
| `status` | `VARCHAR(20)` | False | False | active |
| `commissionable` | `BOOLEAN` | False | False | True |
| `supplier_cost` | `NUMERIC(12, 2)` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`
- Column `extension_tour_id` references `tours.id`

### `tour_gallery_images`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `image_path` | `VARCHAR(255)` | False | False | - |
| `image_title` | `VARCHAR(255)` | False | False |  |
| `image_alt_text` | `VARCHAR(180)` | False | False |  |
| `image_caption` | `TEXT` | True | False |  |
| `image_type` | `VARCHAR(30)` | False | False | gallery |
| `display_order` | `INTEGER` | False | False | 0 |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_group_discount_tiers`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `min_pax` | `INTEGER` | False | False | - |
| `max_pax` | `INTEGER` | False | False | - |
| `discount_type` | `VARCHAR(20)` | False | False | - |
| `discount_value` | `NUMERIC(12, 2)` | False | False | - |
| `status` | `VARCHAR(20)` | False | False | active |
| `funded_by` | `VARCHAR(20)` | False | False | SUPPLIER |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_highlights`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `image` | `VARCHAR(255)` | False | False |  |
| `title` | `VARCHAR(255)` | False | False | - |
| `short_description` | `TEXT` | True | False |  |
| `display_order` | `INTEGER` | False | False | 0 |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_inclusions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `icon` | `VARCHAR(255)` | False | False |  |
| `title` | `VARCHAR(255)` | False | False | - |
| `description` | `TEXT` | True | False |  |
| `display_order` | `INTEGER` | False | False | 0 |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_itineraries`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `day_number` | `INTEGER` | False | False | - |
| `day_title` | `VARCHAR(255)` | False | False |  |
| `location_name` | `VARCHAR(255)` | False | False |  |
| `short_description` | `TEXT` | True | False |  |
| `long_description` | `TEXT` | True | False |  |
| `activities` | `TEXT` | True | False |  |
| `optional_activities` | `TEXT` | True | False |  |
| `accommodation` | `VARCHAR(255)` | True | False |  |
| `start_time` | `VARCHAR(20)` | True | False | - |
| `end_time` | `VARCHAR(20)` | True | False | - |
| `travel_distance` | `VARCHAR(100)` | True | False | - |
| `travel_duration` | `VARCHAR(100)` | True | False | - |
| `transport_type` | `VARCHAR(100)` | True | False | - |
| `meals_included` | `VARCHAR(150)` | True | False | - |
| `important_notes` | `TEXT` | True | False | - |
| `image` | `VARCHAR(255)` | False | False |  |
| `image_alt_text` | `VARCHAR(180)` | False | False |  |
| `images` | `TEXT` | True | False | [] |
| `display_order` | `INTEGER` | False | False | 0 |
| `status` | `VARCHAR(20)` | False | False | active |
| `day_type` | `VARCHAR(20)` | False | False | standard |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_optional_activities`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `activity_name` | `VARCHAR(255)` | False | False | - |
| `description` | `TEXT` | True | False |  |
| `price_per_person` | `NUMERIC(12, 2)` | False | False | 0 |
| `child_price_per_person` | `NUMERIC(12, 2)` | True | False | - |
| `infant_price_per_person` | `NUMERIC(12, 2)` | True | False | - |
| `pricing_mode` | `VARCHAR(20)` | False | False | flat |
| `image` | `VARCHAR(255)` | False | False |  |
| `category` | `VARCHAR(30)` | False | False | other |
| `status` | `VARCHAR(20)` | False | False | active |
| `commissionable` | `BOOLEAN` | False | False | True |
| `supplier_cost` | `NUMERIC(12, 2)` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_overviews`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `duration_text` | `VARCHAR(100)` | False | False |  |
| `start_location` | `VARCHAR(150)` | False | False |  |
| `end_location` | `VARCHAR(150)` | False | False |  |
| `group_size` | `VARCHAR(100)` | False | False |  |
| `tour_type` | `VARCHAR(100)` | False | False |  |
| `vehicle_style` | `VARCHAR(100)` | False | False |  |
| `guide_style` | `VARCHAR(50)` | False | False |  |
| `physical_rating` | `VARCHAR(20)` | False | False | easy |
| `overview_icon_data` | `JSON` | True | False | - |
| `why_choose_this_tour` | `TEXT` | True | False | - |
| `ideal_for` | `TEXT` | True | False | - |
| `best_season` | `VARCHAR(150)` | True | False | - |
| `tour_pace` | `VARCHAR(50)` | True | False | - |
| `transportation_summary` | `TEXT` | True | False | - |
| `accommodation_summary` | `TEXT` | True | False | - |
| `meal_summary` | `TEXT` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_pricing`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `passenger_from` | `INTEGER` | False | False | - |
| `passenger_to` | `INTEGER` | False | False | - |
| `adult_price` | `NUMERIC(12, 2)` | False | False | - |
| `child_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `supplier_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `final_price` | `NUMERIC(12, 2)` | False | False | - |
| `supplier_final_adult_price` | `NUMERIC(12, 2)` | True | False | - |
| `supplier_final_child_price` | `NUMERIC(12, 2)` | True | False | - |
| `commission_percentage` | `NUMERIC(5, 2)` | True | False | - |
| `admin_markup_type` | `VARCHAR(20)` | False | False | percentage |
| `admin_markup_value` | `NUMERIC(12, 2)` | True | False | - |
| `storefront_adult_price` | `NUMERIC(12, 2)` | True | False | - |
| `storefront_child_price` | `NUMERIC(12, 2)` | True | False | - |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_review_comments`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `version_id` | `INTEGER` | True | False | - |
| `section` | `VARCHAR(50)` | False | False | - |
| `field_name` | `VARCHAR(100)` | True | False | - |
| `comment` | `TEXT` | False | False | - |
| `severity` | `VARCHAR(20)` | False | False | minor |
| `status` | `VARCHAR(20)` | False | False | open |
| `created_by` | `INTEGER` | True | False | - |
| `resolved_by` | `INTEGER` | True | False | - |
| `resolved_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`
- Column `resolved_by` references `users.id`
- Column `version_id` references `tour_versions.id`
- Column `created_by` references `users.id`

### `tour_reviews`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `booking_id` | `INTEGER` | False | False | - |
| `customer_id` | `INTEGER` | False | False | - |
| `tour_id` | `INTEGER` | False | False | - |
| `rating` | `INTEGER` | False | False | - |
| `review_text` | `TEXT` | True | False | - |
| `status` | `VARCHAR(30)` | False | False | pending |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `customer_id` references `customers.id`
- Column `booking_id` references `bookings.id`
- Column `tour_id` references `tours.id`

### `tour_similar_tours`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `similar_tour_id` | `INTEGER` | False | False | - |
| `display_order` | `INTEGER` | False | False | 0 |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`
- Column `similar_tour_id` references `tours.id`

### `tour_subcategories`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `category_id` | `INTEGER` | False | False | - |
| `subcategory_name` | `VARCHAR(120)` | False | False | - |
| `slug` | `VARCHAR(150)` | False | False | - |
| `description` | `TEXT` | False | False |  |
| `image` | `VARCHAR(255)` | False | False |  |
| `status` | `VARCHAR(20)` | False | False | active |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `category_id` references `tour_categories.id`

### `tour_subcategory_map`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `subcategory_id` | `INTEGER` | False | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`
- Column `subcategory_id` references `tour_subcategories.id`

### `tour_unavailable_dates`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `unavailable_date` | `DATETIME` | False | False | - |
| `reason` | `TEXT` | True | False |  |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`

### `tour_versions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_id` | `INTEGER` | False | False | - |
| `version_number` | `INTEGER` | False | False | 1 |
| `snapshot` | `JSON` | False | False | - |
| `status` | `VARCHAR(30)` | False | False | pending_approval |
| `change_kind` | `VARCHAR(30)` | False | False | pending_approval |
| `submitted_by` | `INTEGER` | True | False | - |
| `reviewed_by` | `INTEGER` | True | False | - |
| `rejection_reason` | `TEXT` | True | False | - |
| `submitted_at` | `DATETIME` | True | False | - |
| `reviewed_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `tour_id` references `tours.id`
- Column `reviewed_by` references `users.id`
- Column `submitted_by` references `users.id`

### `tours`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `tour_code` | `VARCHAR(30)` | True | False | - |
| `supplier_id` | `INTEGER` | True | False | - |
| `title` | `VARCHAR(180)` | False | False | - |
| `slug` | `VARCHAR(200)` | False | False | - |
| `subtitle` | `VARCHAR(255)` | False | False |  |
| `price_start_per_person` | `NUMERIC(12, 2)` | False | False | 0 |
| `currency` | `VARCHAR(10)` | False | False | USD |
| `country_id` | `INTEGER` | True | False | - |
| `state_id` | `INTEGER` | True | False | - |
| `city_id` | `INTEGER` | True | False | - |
| `category_id` | `INTEGER` | True | False | - |
| `start_location` | `VARCHAR(150)` | False | False |  |
| `finish_location` | `VARCHAR(150)` | False | False |  |
| `number_of_days` | `INTEGER` | False | False | 1 |
| `number_of_hours` | `INTEGER` | True | False | - |
| `number_of_nights` | `INTEGER` | True | False | - |
| `max_group_size` | `INTEGER` | True | False | - |
| `min_booking_size` | `INTEGER` | True | False | - |
| `tour_language` | `VARCHAR(100)` | True | False | - |
| `suitable_age_range` | `VARCHAR(100)` | True | False | - |
| `tour_visibility` | `VARCHAR(20)` | False | False | public |
| `featured` | `BOOLEAN` | False | False | False |
| `short_description` | `TEXT` | False | False |  |
| `long_description` | `TEXT` | False | False |  |
| `pricing_type` | `VARCHAR(20)` | False | False | per_person |
| `offer_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `infant_price` | `NUMERIC(12, 2)` | False | False | 0 |
| `single_supplement` | `NUMERIC(12, 2)` | False | False | 0 |
| `tax_percentage` | `FLOAT` | False | False | 0 |
| `service_fee` | `NUMERIC(12, 2)` | False | False | 0 |
| `gateway_fee_percentage` | `FLOAT` | False | False | 0 |
| `booking_deposit` | `NUMERIC(12, 2)` | False | False | 0 |
| `deposit_type` | `VARCHAR(20)` | False | False | fixed |
| `deposit_percentage` | `FLOAT` | True | False | - |
| `deposit_cutoff_days` | `INTEGER` | True | False | - |
| `balance_payment_deadline_days` | `INTEGER` | True | False | - |
| `requires_supplier_confirmation` | `BOOLEAN` | False | False | True |
| `seo_title` | `VARCHAR(180)` | False | False |  |
| `seo_description` | `VARCHAR(255)` | False | False |  |
| `seo_keywords` | `VARCHAR(255)` | False | False |  |
| `focus_keyword` | `VARCHAR(180)` | True | False | - |
| `canonical_url` | `VARCHAR(500)` | True | False | - |
| `open_graph_image` | `VARCHAR(255)` | True | False | - |
| `search_visibility` | `BOOLEAN` | False | False | True |
| `image_alt_text` | `VARCHAR(180)` | False | False |  |
| `banner_image` | `VARCHAR(255)` | False | False |  |
| `map_image` | `VARCHAR(255)` | False | False |  |
| `mobile_cover_image` | `VARCHAR(255)` | True | False | - |
| `tour_video_url` | `VARCHAR(500)` | True | False | - |
| `brochure_pdf` | `VARCHAR(255)` | True | False | - |
| `status` | `VARCHAR(20)` | False | False | draft |
| `commission_percentage` | `NUMERIC(5, 2)` | True | False | - |
| `admin_markup_percentage` | `NUMERIC(5, 2)` | True | False | - |
| `created_by` | `INTEGER` | True | False | - |
| `updated_by` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `state_id` references `states.id`
- Column `category_id` references `tour_categories.id`
- Column `city_id` references `cities.id`
- Column `country_id` references `countries.id`
- Column `updated_by` references `users.id`
- Column `created_by` references `users.id`
- Column `supplier_id` references `suppliers.id`

### `user_roles`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `user_id` | `INTEGER` | False | False | - |
| `role_id` | `INTEGER` | False | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `user_id` references `users.id`
- Column `role_id` references `roles.id`

### `user_sessions`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `user_id` | `INTEGER` | False | False | - |
| `session_id` | `VARCHAR(120)` | False | False | - |
| `current_refresh_jti` | `VARCHAR(64)` | True | False | - |
| `ip_address` | `VARCHAR(100)` | True | False | - |
| `user_agent` | `VARCHAR(255)` | True | False | - |
| `status` | `VARCHAR(30)` | False | False | active |
| `revoked_at` | `DATETIME` | True | False | - |
| `last_seen_at` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `user_id` references `users.id`

### `user_status_history`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `user_id` | `INTEGER` | False | False | - |
| `from_status` | `VARCHAR(40)` | True | False | - |
| `to_status` | `VARCHAR(40)` | False | False | - |
| `reason` | `VARCHAR(500)` | True | False | - |
| `changed_by` | `INTEGER` | True | False | - |
| `created_at` | `DATETIME` | False | False | - |

**Foreign Keys:**
- Column `changed_by` references `users.id`
- Column `user_id` references `users.id`

### `users`

| Column Name | Data Type | Nullable | Primary Key | Default |
|---|---|---|---|---|
| `id` | `INTEGER` | False | True | - |
| `name` | `VARCHAR(150)` | False | False | - |
| `email` | `VARCHAR(150)` | False | False | - |
| `phone` | `VARCHAR(30)` | False | False |  |
| `profile_image` | `VARCHAR(255)` | False | False |  |
| `address` | `VARCHAR(255)` | False | False |  |
| `country` | `VARCHAR(100)` | False | False |  |
| `state` | `VARCHAR(100)` | False | False |  |
| `city` | `VARCHAR(100)` | False | False |  |
| `pincode` | `VARCHAR(20)` | False | False |  |
| `password` | `VARCHAR(255)` | True | False | - |
| `role_id` | `INTEGER` | True | False | - |
| `is_active` | `BOOLEAN` | True | False | True |
| `approval_status` | `VARCHAR(30)` | False | False | approved |
| `user_type` | `VARCHAR(20)` | True | False | - |
| `country_code` | `VARCHAR(8)` | False | False |  |
| `mobile_number` | `VARCHAR(20)` | True | False | - |
| `email_verified` | `BOOLEAN` | False | False | False |
| `password_created_at` | `DATETIME` | True | False | - |
| `account_status` | `VARCHAR(40)` | False | False | ACTIVE |
| `admin_verified` | `BOOLEAN` | False | False | False |
| `admin_verified_at` | `DATETIME` | True | False | - |
| `admin_verified_by` | `INTEGER` | True | False | - |
| `deactivated_at` | `DATETIME` | True | False | - |
| `deactivated_by` | `INTEGER` | True | False | - |
| `deactivation_reason` | `VARCHAR(500)` | True | False | - |
| `last_login_at` | `DATETIME` | True | False | - |
| `reset_password_token` | `VARCHAR(255)` | True | False | - |
| `reset_password_expires_at` | `DATETIME` | True | False | - |
| `email_verified_at` | `DATETIME` | True | False | - |
| `email_verification_token` | `VARCHAR(255)` | True | False | - |
| `email_verification_expires_at` | `DATETIME` | True | False | - |
| `otp_code_hash` | `VARCHAR(255)` | True | False | - |
| `otp_expires_at` | `DATETIME` | True | False | - |
| `otp_attempts` | `INTEGER` | True | False | 0 |
| `token_version` | `INTEGER` | False | False | 0 |
| `two_factor_enabled` | `BOOLEAN` | False | False | False |
| `two_factor_secret` | `VARCHAR(255)` | True | False | - |
| `two_factor_backup_codes` | `TEXT` | True | False | - |
| `force_password_reset` | `BOOLEAN` | False | False | False |
| `failed_login_attempts` | `INTEGER` | False | False | 0 |
| `locked_until` | `DATETIME` | True | False | - |
| `created_at` | `DATETIME` | True | False | - |
| `updated_at` | `DATETIME` | True | False | - |

**Foreign Keys:**
- Column `role_id` references `roles.id`
- Column `deactivated_by` references `users.id`
- Column `admin_verified_by` references `users.id`

---

# Chapter 05 — Database Migration Readiness

## 1. Migration History & Current Head

Database migrations for the Tourvaa platform are managed via **Alembic**.

### Migration State Summary
- **Current Head Migration**: [alembic/versions/20261028_0054_financial_document_snapshots.py](../../../tourvaa-admin-backend/alembic/versions/20261028_0054_financial_document_snapshots.py)
- **Total Migrations Tracked**: 118 revision files.
- **Pending Migrations for Step 7 Fixes**: **0 (None)**.
- **Verification Rule**: In `app/main.py`, the `validate_database_migration_head()` function executes during the application lifespan and checks `alembic_version` against the migration tree. If any pending migrations exist, the backend will fail to boot with an explicit error.

---

## 2. Table Schema Compatibility & Integrity

The canonical source-level inventory records 138 ORM application tables; a deployed MySQL schema also contains Alembic's `alembic_version` table. The live physical count must still be checked against the target database immediately before migration.
Key structural guarantees verified:
1. **Foreign Key Integrity**: All foreign key relationships (`bookings.customer_id`, `tours.supplier_id`, `invoices.booking_id`, etc.) use explicit `ON DELETE` constraints to prevent orphaned records.
2. **Unique Constraints**: Unique indexes protect user emails, role slugs, booking reference numbers, and voucher codes.
3. **Transaction Safety**: All database operations executed via FastAPI dependency injection use the protected `get_db()` session generator, ensuring automatic rollback on unhandled exceptions.

---

## 3. Database Migration Deployment Runbook

When deploying migrations to a new environment or staging cluster:

```bash
# 1. Use a protected MySQL defaults file or mounted secret; never pass passwords in argv.
# Example defaults file: /run/secrets/tourvaa-mysql.cnf (mode 0600)
mysqldump --defaults-extra-file=/run/secrets/tourvaa-mysql.cnf --single-transaction --routines --triggers tourvaa > pre_migration_backup.sql

# 2. Check current database revision vs head
python -m alembic current
python -m alembic heads

# 3. Apply pending migrations
python -m alembic upgrade head

# 4. Verify head matches code
python -m alembic current --check-heads
```

### Critical Rollback Strategy & MySQL Non-Transactional DDL Limitation
> [!CAUTION]
> **MySQL InnoDB Non-Transactional DDL**: In MySQL (including 8.0 and 8.4), DDL statements (`CREATE TABLE`, `ALTER TABLE`, `DROP TABLE`, `CREATE INDEX`, `DROP INDEX`) execute with **implicit commits** before and after execution. Multi-statement migrations do **NOT** execute inside an atomic rollback transaction.

If an Alembic migration script fails halfway (e.g. the 2nd `ALTER TABLE` statement fails):
1. **Partial Application State**: The 1st statement remains committed in the database, while subsequent statements have not run.
2. **Alembic Version Status**: Alembic does NOT update `alembic_version` on a failed migration; the database remains registered at the previous revision.
3. **Automatic Rollback Failure**: Re-running `alembic upgrade head` or `alembic downgrade` will fail because the partially applied changes are already present.

#### Required Recovery Procedures for Failed Migrations:
- **Approach A (Recommended — Full Restoration)**:
  Restore the database immediately from the pre-migration snapshot:
  ```bash
  mysql --defaults-extra-file=/run/secrets/tourvaa-mysql.cnf tourvaa < pre_migration_backup.sql
  ```
- **Approach B (Forensic Manual DDL Reversal)**:
  If restoring a large database is prohibitive, inspect the failed migration script, identify which statements succeeded, and manually execute the corresponding reverse DDL (e.g., `ALTER TABLE table DROP COLUMN col;`) in the MySQL CLI before investigating the root cause and re-running the migration.