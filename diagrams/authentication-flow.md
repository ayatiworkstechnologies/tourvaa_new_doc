# Authentication & Authorization Decision Flow

This document details the authentication and authorization lifecycle in Tourvaa, encompassing credential login, dual-domain JWT validation, 2FA with TOTP, session tracking, password reset token rotation, and RBAC permission checks.

---

## 1. Login & Token Lifecycle Sequence Diagram

```mermaid
sequenceDiagram
    autonumber
    actor User as User / Portal Visitor
    participant Browser as Web Browser
    participant FE as Next.js Frontend
    participant API as FastAPI Backend (/api/auth)
    participant DB as MySQL Database
    participant SMTP as SMTP Mailer

    User->>Browser: Enters Email & Password
    Browser->>FE: Submit Form Data
    FE->>API: POST /api/auth/login (email, password)
    
    API->>DB: Query User by Email
    alt User Not Found or Inactive
        API-->>FE: 401 Unauthorized ("Invalid credentials")
    end

    alt Account Locked (locked_until > now)
        API-->>FE: 403 Forbidden ("Account locked due to failed attempts")
    end

    API->>API: verify_password(plaintext, stored_bcrypt_hash)
    alt Password Invalid
        API->>DB: Increment failed_login_attempts
        opt failed_login_attempts >= 5
            API->>DB: Set locked_until = now() + 15 minutes
        end
        API-->>FE: 401 Unauthorized ("Invalid credentials")
    end

    API->>DB: Reset failed_login_attempts = 0

    alt 2FA Enabled on Account
        API-->>FE: 200 OK (requires_2fa: true, temp_token: JWT)
        FE->>User: Prompt for 6-Digit TOTP / Backup Code
        User->>FE: Enter OTP
        FE->>API: POST /api/auth/2fa/verify (temp_token, code)
        API->>API: Verify TOTP via pyotp or validate backup code
    end

    API->>API: Determine Role & Portal (admin vs normal domain)
    API->>API: Sign Access JWT (exp: 24h) with domain secret
    API->>API: Sign Refresh JWT (exp: 30d, jti: uuid4)
    
    API->>DB: Insert into user_sessions (user_id, jti, ip, user_agent, expires_at)
    API->>DB: Insert into login_history (status: success)
    
    API-->>FE: Set httpOnly cookies: 'tourvaa_access' & 'tourvaa_refresh'
    API-->>FE: Return user profile JSON
    
    FE->>FE: Update AuthProvider State
    FE->>Browser: Redirect to User Portal Dashboard
```

---

## 2. Authorization Decision Flowchart

```mermaid
flowchart TD
    START([Incoming API Request]) --> EXTRACT[Extract Token from Cookie or Bearer Header]
    EXTRACT --> TOKEN_EXISTS{Token Present?}
    
    TOKEN_EXISTS -- No --> PUBLIC_CHECK{Is Route Public?}
    PUBLIC_CHECK -- Yes --> ALLOW_PUBLIC[Execute Endpoint Handler]
    PUBLIC_CHECK -- No --> DENY_401[401 Unauthorized]
    
    TOKEN_EXISTS -- Yes --> DECODE[decode_auth_token: Check Admin & Normal Secrets]
    DECODE --> SIGNATURE_VALID{Signature Valid?}
    SIGNATURE_VALID -- No --> EXPIRED_CHECK{Signature Expired?}
    EXPIRED_CHECK -- Yes --> DENY_401_EXP[401 Token Expired]
    EXPIRED_CHECK -- No --> DENY_401_INV[401 Invalid Token]
    
    SIGNATURE_VALID -- Yes --> FETCH_USER[Fetch User & Role from Database]
    FETCH_USER --> USER_ACTIVE{user.is_active == 1?}
    USER_ACTIVE -- No --> DENY_DEACTIVE[403 Account Deactivated]
    
    USER_ACTIVE -- Yes --> VERSION_CHECK{token_version == user.token_version?}
    VERSION_CHECK -- No --> DENY_REVOKED[401 Session Revoked - Password Changed]
    
    VERSION_CHECK -- Yes --> SESSION_DB_CHECK{UserSession Active & Not Revoked?}
    SESSION_DB_CHECK -- No --> DENY_SESSION_REVOKED[401 Session Terminated]
    
    SESSION_DB_CHECK -- Yes --> APPROVAL_CHECK{Partner Role Requires Approval?}
    APPROVAL_CHECK -- Supplier --> SUP_APPROVED{supplier.approval_status == 'approved'?}
    APPROVAL_CHECK -- Agent --> AGT_APPROVED{agent.approval_status == 'approved'?}
    APPROVAL_CHECK -- Affiliate --> AFF_APPROVED{affiliate.status == 'approved'?}
    APPROVAL_CHECK -- Other --> PERMISSION_GATE
    
    SUP_APPROVED -- No --> SAFE_SUP_CHECK{Prefix in PENDING_SUPPLIER_SAFE?}
    SAFE_SUP_CHECK -- Yes --> PERMISSION_GATE
    SAFE_SUP_CHECK -- No --> DENY_SUP_APP[403 SUPPLIER_APPROVAL_REQUIRED]
    
    AGT_APPROVED -- No --> SAFE_AGT_CHECK{Prefix in PENDING_AGENT_SAFE?}
    SAFE_AGT_CHECK -- Yes --> PERMISSION_GATE
    SAFE_AGT_CHECK -- No --> DENY_AGT_APP[403 AGENT_APPROVAL_REQUIRED]

    AFF_APPROVED -- No --> DENY_AFF_APP[403 AFFILIATE_APPROVAL_REQUIRED]
    
    SUP_APPROVED -- Yes --> PERMISSION_GATE
    AGT_APPROVED -- Yes --> PERMISSION_GATE
    AFF_APPROVED -- Yes --> PERMISSION_GATE
    
    PERMISSION_GATE[Evaluate Endpoint Permission Requirement] --> SUPER_ADMIN_CHECK{user.role == 'super-admin'?}
    SUPER_ADMIN_CHECK -- Yes --> GRANT_ACCESS[Allow Request Execution]
    
    SUPER_ADMIN_CHECK -- No --> HAS_PERM{User Role has Required Permission Slug?}
    HAS_PERM -- Yes --> GRANT_ACCESS
    HAS_PERM -- No --> DENY_403[403 Forbidden: Insufficient Permissions]
```

---

## 3. Key Security Properties

1. **Dual Cryptographic Domains**:
   - The administration interface uses `ADMIN_JWT_SECRET_KEY`.
   - External portal users (customers, suppliers, agents, affiliates) use `NORMAL_JWT_SECRET_KEY`.
   - Even if a customer obtains a valid token, it is cryptographically rejected by administrative endpoints because the token domain claim is strictly verified.
2. **Revocation via `token_version`**:
   - When a user changes their password or clicks "Sign out everywhere", the database increments `user.token_version`.
   - All outstanding JWTs become instantly invalid, preventing session replay.
3. **Defense Against Brute Force**:
   - Consecutive login failures are counted in `failed_login_attempts`.
   - Upon the 5th failed attempt, `locked_until` is populated with `now() + 15 minutes`.
   - The API short-circuits attempts during lockout without verifying the password, mitigating timing attacks.
