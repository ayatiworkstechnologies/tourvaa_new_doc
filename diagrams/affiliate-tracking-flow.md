# Affiliate Referral Tracking & Commission Workflow

This document details the tracking, attribution, commission calculation, and wallet payout mechanics of the Tourvaa Affiliate Marketing system.

---

## 1. Affiliate Referral & Attribution Architecture Diagram

```mermaid
sequenceDiagram
    autonumber
    actor Visitor as Prospective Traveller
    actor Affiliate as Marketing Partner
    participant ShortLink as Short Redirect (/r/{code})
    participant FE as Next.js Storefront
    participant API as FastAPI Backend
    participant DB as MySQL Database
    participant Worker as Commission Engine

    Affiliate->>API: POST /api/affiliate/links (create custom link)
    API->>DB: Insert AffiliateLink (code: 'PROMO2026', attribution_window: 30 days)
    API-->>Affiliate: Link Created: https://tourvaa.com/r/PROMO2026

    Visitor->>ShortLink: Clicks https://tourvaa.com/r/PROMO2026
    ShortLink->>DB: Insert AffiliateClick (ip, user_agent, referrer, clicked_at)
    ShortLink->>DB: Increment AffiliateLink.clicks_count
    ShortLink-->>Visitor: HTTP 307 Redirect to Destination URL with Cookie 'tv_aff_code'

    Visitor->>FE: Browses Tours & Decides to Book
    FE->>API: POST /api/checkout/create-session (Payload includes referral cookie)
    API->>DB: Query AffiliateLink by code
    API->>DB: Validate Attribution Window (click_time + window_days >= now)
    
    alt Attribution Valid
        API->>DB: Insert AffiliateAttribution (affiliate_id, link_id, booking_id)
        API->>DB: Set Booking.affiliate_attribution_id
    end

    Note over Visitor, Worker: Booking Confirmed & Payment Captured
    API->>Worker: Trigger Affiliate Commission Calculation
    Worker->>DB: Query AffiliateCommissionRule for Tour / Affiliate Tier
    Worker->>Worker: compute_commission(eligible_amount, rule_type, percentage/flat)
    Worker->>DB: Insert AffiliateConversion (status: 'pending_hold')
    
    Note over Worker, DB: Tour Completed & Dispute Window Elapsed (e.g. 14 Days)
    Worker->>DB: Transition Conversion status -> 'approved'
    Worker->>DB: Credit Affiliate Wallet Balance (AffiliateWalletTransaction)
    Worker->>Affiliate: Email Notification: "Commission Earned"

    Affiliate->>API: POST /api/affiliate/payouts (request payout to bank/PayPal)
    API->>DB: Verify Wallet Balance >= payout_amount
    API->>DB: Deduct Wallet & Insert AffiliatePayout (status: 'pending')
    
    Admin->>API: POST /api/admin/affiliates/payouts/{id}/approve
    API->>DB: Update AffiliatePayout status -> 'paid'
    API->>Affiliate: Dispatch Payout Confirmation Email
```

---

## 2. Commission Calculation Rules & Slabs

- **Rule Types**: Supports both `percentage` (e.g. 5% of net tour price) and `fixed` amounts (e.g. $50 per booking).
- **Attribution Logic**: First-touch or last-touch attribution within configurable attribution windows (default: 30 days).
- **Fraud Prevention**: Commissions remain in `pending_hold` status until the tour travel date has completed and cancellation dispute periods have expired. Cancelled or refunded bookings automatically invalidate associated pending conversions.
