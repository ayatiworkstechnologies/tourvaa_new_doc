# Payment Pre-Authorization, Hold & Capture Flow

This document details the payment gateway interaction architecture for Stripe and PayPal, demonstrating how funds are pre-authorized upon checkout, held in escrow during supplier evaluation, captured upon final confirmation, or released/refunded upon rejection or cancellation.

---

## 1. Payment Lifecycle Architecture Diagram

```mermaid
flowchart TD
    CHECKOUT[Customer Initiates Checkout] --> SELECT_GATEWAY{Choose Payment Method}
    
    SELECT_GATEWAY -->|Stripe Credit/Debit Card| STRIPE_SESSION["Stripe Checkout Session<br/>payment_intent_data: capture_method='manual'"]
    SELECT_GATEWAY -->|PayPal Account / Card| PAYPAL_ORDER["PayPal v2 Order<br/>intent='AUTHORIZE'"]

    STRIPE_SESSION --> CUST_AUTH_STRIPE[Customer Approves Card in Stripe]
    PAYPAL_ORDER --> CUST_AUTH_PAYPAL[Customer Authorizes via PayPal]

    CUST_AUTH_STRIPE --> STRIPE_WEBHOOK["Webhook: checkout.session.completed"]
    CUST_AUTH_PAYPAL --> PAYPAL_CAPTURE["GET /api/payments/paypal/capture"]

    STRIPE_WEBHOOK --> RECORD_HOLD["Insert PaymentHold and Payment status='authorized'"]
    PAYPAL_CAPTURE --> RECORD_HOLD

    RECORD_HOLD --> DECISION_GATE{Supplier Decision within 4 Days?}

    DECISION_GATE -->|"Accepted by Supplier & Confirmed by Admin"| CAPTURE_FUNDS[Capture Authorized Funds]
    DECISION_GATE -->|"Declined or Decision Window Expired"| RELEASE_FUNDS[Release Authorized Hold]

    subgraph CAPTURE_FLOW["Payment Capture Workflow"]
        CAPTURE_FUNDS --> DO_CAPTURE{Provider?}
        DO_CAPTURE -->|Stripe| STRIPE_POST["POST /v1/payment_intents/{id}/capture"]
        DO_CAPTURE -->|PayPal| PAYPAL_POST["POST /v2/payments/authorizations/{id}/capture"]
        STRIPE_POST --> CAPTURE_SUCCESS{Success?}
        PAYPAL_POST --> CAPTURE_SUCCESS
        CAPTURE_SUCCESS -->|Yes| MARK_PAID["Update Payment status='completed'<br/>Generate Confirmation Receipt<br/>Generate Invoice"]
        CAPTURE_SUCCESS -->|No| CAPTURE_RETRY["Schedule in _payment_capture_retry_loop<br/>Retried every 15 minutes"]
    end

    subgraph RELEASE_FLOW["Authorization Release / Void Workflow"]
        RELEASE_FUNDS --> DO_CANCEL{Provider?}
        DO_CANCEL -->|Stripe| STRIPE_CANCEL["POST /v1/payment_intents/{id}/cancel"]
        DO_CANCEL -->|PayPal| PAYPAL_VOID["POST /v2/payments/authorizations/{id}/void"]
        STRIPE_CANCEL --> VOID_SUCCESS["PaymentHold status='released'<br/>Payment status='voided'<br/>Seats released back to TourCalendar"]
        PAYPAL_VOID --> VOID_SUCCESS
    end

    subgraph REFUND_FLOW["Post-Capture Refund Workflow"]
        MARK_PAID -.->|Customer Cancels Later| REFUND_CHECK{Refund Rule Evaluation}
        REFUND_CHECK --> EXEC_REFUND{Provider?}
        EXEC_REFUND -->|Stripe| STRIPE_REFUND["POST /v1/refunds with idempotency key"]
        EXEC_REFUND -->|PayPal| PAYPAL_REFUND["POST /v2/payments/captures/{id}/refund"]
        STRIPE_REFUND --> REFUND_COMPLETE["Payment status='refunded'<br/>Debit Supplier Ledger<br/>Issue Credit Note"]
        PAYPAL_REFUND --> REFUND_COMPLETE
    end
```

---

## 2. Key Gateway Integration Mechanisms

### 2.1 Webhook Signature Validation
1. **Stripe Webhook (`construct_event`)**:
   - Parses the `Stripe-Signature` header for timestamp `t` and signature `v1`.
   - Computes HMAC-SHA256 signature using `STRIPE_WEBHOOK_SECRET` over `${t}.${raw_body}`.
   - Rejects stale webhooks where `abs(time.time() - int(t)) > 300` (5-minute replay defense).
   - Validates using constant-time string comparison (`hmac.compare_digest`).

2. **PayPal Webhook (`verify_webhook_signature`)**:
   - Compares incoming transmission headers (`PAYPAL-AUTH-ALGO`, `PAYPAL-TRANSMISSION-ID`, `PAYPAL-CERT-URL`, `PAYPAL-TRANSMISSION-SIG`, `PAYPAL-TRANSMISSION-TIME`).
   - Verifies against `PAYPAL_WEBHOOK_ID` configured for the production API endpoint.

### 2.2 Idempotency & Fault Tolerance
- All Stripe captures, voids, and refunds supply a unique `Idempotency-Key` (e.g. `capture-{payment.id}-{attempt}`).
- If gateway capture fails due to temporary network partitions after supplier acceptance, the record enters retry state and is automatically re-attempted by `_payment_capture_retry_loop()` every 15 minutes.
