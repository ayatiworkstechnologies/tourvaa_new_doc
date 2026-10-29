# Booking Lifecycle & State Transition Workflow

This document models the complete booking lifecycle in Tourvaa, detailing the state machine, seat reservation mechanics, supplier acceptance requirements, payment hold-to-capture sequence, and customer receipt generation.

---

## 1. Booking State Transition Diagram

```mermaid
stateDiagram-v2
    [*] --> draft: Customer initiates booking

    draft --> pending_payment: Checkout started
    draft --> cancelled: Abandoned

    pending_payment --> payment_authorized: Gateway Pre-Auth Hold
    pending_payment --> pending_supplier_assignment: Unassigned / Agent Booking
    pending_payment --> cancelled: Stale Unpaid Expiry (60m)

    payment_authorized --> pending_supplier_acceptance: Supplier Notified
    pending_supplier_assignment --> pending_supplier_acceptance: Admin Assigns Supplier

    pending_supplier_acceptance --> supplier_accepted: Supplier Accepts Request
    pending_supplier_acceptance --> supplier_reassignment_required: Supplier Declines
    pending_supplier_acceptance --> cancelled: 4-Day Hold Expiry Sweep

    supplier_reassignment_required --> pending_supplier_assignment: Admin Reassigns
    supplier_reassignment_required --> declined: No Alternative Supplier

    supplier_accepted --> confirmed: Tourvaa Admin Confirms & Gateway Captures
    supplier_accepted --> cancelled: Pre-Confirmation Cancellation

    confirmed --> ready_to_travel: Voucher & Receipt Issued
    ready_to_travel --> ongoing: Tour Departure Date Reached
    ongoing --> completed: Tour End Date Reached

    confirmed --> cancellation_requested: Customer / Agent Requests Cancellation
    cancellation_requested --> confirmed: Cancellation Rejected
    cancellation_requested --> cancelled: Cancellation Approved (Refund Applied)
    
    declined --> refunded: Gateway Pre-Auth Released / Refunded
    cancelled --> refunded: Funds Credited to Customer

    completed --> [*]
    refunded --> [*]
```

---

## 2. End-to-End Booking Sequence Walkthrough

```mermaid
sequenceDiagram
    autonumber
    actor Cust as Customer / Agent
    participant FE as Next.js Storefront / Portal
    participant API as FastAPI Backend
    participant DB as MySQL Database
    participant Stripe as Stripe Gateway
    participant Sup as Supplier Portal
    participant Admin as Tourvaa Operations
    participant Worker as Background Sweeper

    Cust->>FE: Select Tour & Travel Date
    FE->>API: GET /api/tours/{id}/availability-schedule
    API->>DB: Query TourCalendar (available_seats >= passenger_count)
    API-->>FE: Return Departure Slots & Pricing
    
    Cust->>FE: Fill Traveller Details & Click "Reserve"
    FE->>API: POST /api/checkout/create-session
    API->>DB: Insert Booking (status: 'draft', payment_status: 'unpaid')
    API->>DB: Decrement TourCalendar available_seats (Hold seats)
    API->>Stripe: Create Checkout Session (capture_method: 'manual')
    API-->>FE: Return Stripe Checkout URL & Booking Code

    Cust->>Stripe: Approves Card Authorization
    Stripe-->>API: Webhook (checkout.session.completed)
    API->>DB: Insert PaymentHold & Payment (status: 'authorized')
    API->>DB: Transition Booking -> 'payment_authorized'
    API->>DB: Notify Assigned Supplier (Notification & Email)
    API->>DB: Transition Booking -> 'pending_supplier_acceptance'

    alt Supplier Accepts within 4 Days
        Sup->>API: POST /api/bookings/{id}/supplier-decision (action: 'accept')
        API->>DB: Transition Booking -> 'supplier_accepted'
        API->>Admin: Notify Tourvaa Operations ("Supplier accepted booking")
        
        Admin->>API: POST /api/bookings/{id}/confirm
        API->>Stripe: POST /v1/payment_intents/{id}/capture (Capture Authorized Hold)
        API->>DB: Update Payment (status: 'completed', amount_paid: full/deposit)
        API->>DB: Transition Booking -> 'confirmed'
        API->>DB: Generate Confirmation Receipt PDF (confirmation_receipts.py)
        API->>DB: Generate Customer Invoice (invoices.py)
        API->>Cust: Dispatch Booking Confirmation Email with Attached PDF Receipt
        API->>DB: Credit Supplier Ledger (Net tour cost less commission)
    else Supplier Declines or Times Out
        Worker->>API: _payment_hold_loop() runs (every 60m)
        Worker->>Stripe: Cancel PaymentIntent (Release Card Authorization Hold)
        Worker->>DB: Release TourCalendar seats
        Worker->>DB: Transition Booking -> 'cancelled' / 'declined'
        Worker->>Cust: Send Apology Email & Offer Alternative Dates
    end
```

---

## 3. Critical Business Rules Verified from Source Code

1. **Payment Authorization Is Not Final Confirmation**:
   - As stated in [`app/services/payments.py`](../../tourvaa-admin-backend/app/services/payments.py) line 21: *"A payment authorization is not a receipt and supplier acceptance is not the customer-facing final confirmation."*
   - Stripe card authorizations use `capture_method="manual"` to place an authorized hold without debiting the customer immediately.
2. **Four-Day Supplier Decision Window**:
   - The automated background worker `_payment_hold_loop()` periodically cancels authorizations before they expire on the gateway, preventing funds from hanging in customer bank accounts if a supplier is unresponsive.
3. **Seat Holding & Stale Booking Expiry**:
   - Unpaid bookings in `pending_payment` hold seats in `TourCalendar`. The coroutine `_expire_stale_bookings_loop()` runs every 15 minutes and automatically releases seats if payment is not authorized within `BOOKING_EXPIRY_HOLD_MINUTES` (60 minutes).
4. **Immutable Confirmation Receipts**:
   - Final booking receipts (`booking-confirmation-{id}-v2.pdf`) are stored in `private-docs/booking-confirmations/` upon initial confirmation. They are immutable snapshots and are never dynamically recomputed from mutable database rows on later download.
