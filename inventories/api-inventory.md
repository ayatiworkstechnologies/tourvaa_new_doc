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
