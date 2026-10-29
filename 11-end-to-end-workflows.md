# 11 — End-to-End Business Workflows

This document traces ten critical user journeys through the entire application stack: **User Action → Frontend Component → API Request → Authentication → Backend Router → Business Service → Database Operation → API Response → UI Update**.

---

## Journey 1: Customer Tour Discovery, Checkout & Pre-Authorization
1. **User Action**: Customer browses `/tours/[id]`, picks a departure date with available seats, adds traveller details, and clicks "Reserve Tour".
2. **Frontend Component**: `TourBookingWidget` dispatches `POST /api/checkout/create-session`.
3. **Backend Service**: `app/services/checkout.py` validates seat availability in `TourCalendar`, decrements seat quota, creates a `Booking` record in `draft` status, and creates a Stripe Checkout Session with `capture_method='manual'`.
4. **Database Operation**: Inserts `bookings`, `booking_travellers`, and `checkout_sessions`.
5. **Gateway Interaction**: Stripe redirects customer to hosted card payment page. Customer authorizes card.
6. **Webhook Handling**: Stripe emits `checkout.session.completed`. `app/services/payments.py` records a `PaymentHold` and updates booking status to `payment_authorized`.
7. **Notification**: Enqueues email to assigned supplier: *"New booking request awaiting your acceptance"*.

---

## Journey 2: Supplier Acceptance & Tourvaa Final Confirmation
1. **User Action**: Supplier logs into `/supplier/bookings/[id]` and clicks "Accept Booking Request".
2. **Backend Processing**: `app/services/bookings.py` validates supplier ownership and transitions booking to `supplier_accepted`.
3. **Admin Review**: Tourvaa administrator navigates to `/admin/bookings/[id]` and clicks "Confirm Booking & Capture Funds".
4. **Gateway Capture**: `app/services/payments.py` calls Stripe `POST /v1/payment_intents/{id}/capture`.
5. **Receipt Generation**: `app/services/confirmation_receipts.py` generates `booking-confirmation-{id}-v2.pdf` and saves to `private-docs/booking-confirmations/`.
6. **Customer Receipt**: Customer receives email with attached confirmation receipt and booking status becomes `confirmed`.
7. **Ledger Credit**: Net tour amount (tour price minus Tourvaa platform commission) is credited to `supplier_ledgers`.

---

## Journey 3: B2B Travel Agent Client Reservation
1. **User Action**: Agent navigates to `/agent/tours`, selects a package, and enters client traveller details with custom agent markup.
2. **Backend Service**: `app/services/agents.py` checks agent credit limits and buffer rules.
3. **Financial Snapshot**: Records net wholesale tour cost, agent commission tier, and retail client total.
4. **Ledger Recording**: Commission is recorded in `agent_ledger`. Booking is assigned to supplier.

---

## Journey 4: Affiliate Referral Tracking & Commission Conversion
1. **Visitor Action**: Visitor clicks affiliate short-link `https://tourvaa.com/r/SUMMER26`.
2. **Redirect Processing**: `app/routers/affiliate_redirect.py` logs `AffiliateClick` and sets `tv_aff_code` cookie with 30-day expiration.
3. **Checkout Conversion**: When visitor completes checkout, `app/services/affiliate_tracking.py` attributes booking to the affiliate.
4. **Wallet Credit**: Upon tour completion, commission is calculated and credited to the affiliate's wallet balance.

---

## Journey 5: Supplier Tour Update & Version Approval
1. **Supplier Edit**: Supplier modifies itinerary in `/supplier/tours/[id]/edit` and submits for review.
2. **Version Creation**: `app/services/tour_versions.py` takes a complete JSON snapshot into `tour_versions` (`pending_approval`). Live tour is untouched.
3. **Admin Inspection**: Admin views visual diff in `/admin/tour-approval`.
4. **Approval**: Admin clicks "Approve Changes". The snapshot is applied to the live tour record in `tours`.

---

## Journey 6: Customer Cancellation Request & Gateway Refund
1. **Customer Action**: Customer requests cancellation in `/customer/cancellations`.
2. **Policy Evaluation**: `app/services/cancellations.py` checks cancellation policy rules against departure date.
3. **Refund Execution**: Admin approves. Service calls Stripe/PayPal refund API with idempotency key.
4. **Ledger Adjustment**: Payment marked `refunded`, calendar seats restored, and supplier ledger debited.

---

## Journey 7: AI Chatbot Query & Tour Recommendation
1. **User Query**: Visitor asks *"What tours do you offer in New Zealand for 7 days?"* in floating widget.
2. **Vector Embedding**: FastEmbed generates embedding vector on CPU.
3. **RAG Retrieval**: Calculates cosine similarity against `chat_embeddings` in MySQL.
4. **Response**: Returns grounded answer along with clickable tour recommendation cards.

---

## Journey 8: Realtime Support Chat & WebSocket Message
1. **User Action**: Customer types message on booking thread `/customer/support`.
2. **REST Ingestion**: `POST /api/messaging/threads/{id}/messages` saves message to database.
3. **Redis Pub/Sub**: Publishes event to `ws:messages`.
4. **WebSocket Delivery**: Uvicorn worker hosting supplier/admin socket pushes frame live to browser.

---

## Journey 9: Automated Stale Unpaid Booking Expiry
1. **Scheduled Tick**: Coroutine `_expire_stale_bookings_loop` runs every 15 minutes.
2. **Lock Acquisition**: Takes distributed Redis lock `expire_stale_bookings`.
3. **Seat Release**: Identifies bookings in `pending_payment` older than 60 minutes. Transitions status to `cancelled` and increments `TourCalendar.available_seats`.

---

## Journey 10: Scheduled Financial Sales Report
1. **Scheduled Tick**: Coroutine `_report_schedule_loop` triggers at 00:00 UTC.
2. **Aggregation**: Aggregates daily sales, gateway fees, and commission earnings.
3. **Export**: Generates OpenPyXL spreadsheet.
4. **Email Delivery**: Dispatches email to administrative stakeholders via SMTP.
