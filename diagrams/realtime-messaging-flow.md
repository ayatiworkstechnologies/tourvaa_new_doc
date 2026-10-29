# Realtime WebSocket Messaging & Notification Flow

This document details the WebSocket architecture in Tourvaa, explaining the ticket minting protocol, cross-worker Redis pub/sub messaging, presence tracking, and conversation thread synchronization.

---

## 1. WebSocket Connection & Messaging Architecture

```mermaid
sequenceDiagram
    autonumber
    actor Client as Browser Client
    participant Proxy as Next.js Edge Proxy
    participant REST as FastAPI REST API
    participant WS as FastAPI WebSocket Hub
    participant Redis as Redis Pub/Sub (ws:messages)
    participant Worker2 as Sibling Uvicorn Worker
    participant DB as MySQL Database

    Note over Client, REST: Step 1: Secure Handshake Authentication
    Client->>Proxy: POST /api/messaging/ws/ticket (with tourvaa_access cookie)
    Proxy->>REST: Forward to /api/messaging/ws/ticket
    REST->>REST: Authenticate user & mint ticket (30s TTL UUID)
    REST->>Redis: SETEX ws:ticket:{ticket} 30 {user_id, role, portal}
    REST-->>Client: Return JSON { ticket: "uuid4_single_use" }

    Note over Client, WS: Step 2: Direct WebSocket Connection
    Client->>WS: WebSocket Upgrade: wss://backend/api/ws/messages?ticket=uuid4
    WS->>Redis: GETDEL ws:ticket:{ticket} (Atomic Redemption)
    alt Ticket Invalid or Expired
        WS-->>Client: Close Socket (Code 4001: Unauthorized)
    end
    WS->>WS: Register connection in UserSocketRegistry[user_id]
    WS-->>Client: Accept Connection & Send Ready Event

    Note over Client, DB: Step 3: Message Posting & Cross-Worker Broadcast
    Client->>REST: POST /api/messaging/threads/{id}/messages (text, attachment)
    REST->>DB: Insert Message into database
    REST->>DB: Commit Transaction
    REST->>Redis: PUBLISH ws:messages { event: 'new_message', thread_id, payload }

    par Worker 1 (Hosting Sender Socket)
        Redis-->>WS: Ingest Pub/Sub frame
        WS->>Client: Send WebSocket JSON Frame (Message Delivered)
    and Worker 2 (Hosting Recipient Socket)
        Redis-->>Worker2: Ingest Pub/Sub frame
        Worker2->>Worker2: Lookup recipient user_id in local socket registry
        Worker2->>Client: Send WebSocket JSON Frame (Message Received Live)
    end
```

---

## 2. Technical Highlights

1. **Ticket-Based Handshake**:
   - Web browsers cannot set custom headers during native `new WebSocket()` upgrades.
   - Cross-origin WebSocket handshakes bypass the Next.js same-origin rewrite proxy.
   - Tourvaa mints a single-use, 30-second Redis-backed ticket via an authenticated same-origin REST request, then passes it as a query param. The ticket is immediately destroyed upon connection (`GETDEL`).
2. **Multi-Worker Scaling via Redis**:
   - In production environments where `WEB_CONCURRENCY > 1`, user sockets are distributed across different OS processes.
   - The Redis pub/sub channel `ws:messages` guarantees that any message published by worker A immediately broadcasts to worker B holding the recipient's socket.
3. **Presence & Heartbeats**:
   - Sockets emit periodic ping/pong frames (`PRESENCE_TTL_SECONDS = 75`).
   - Connections are capped at `MAX_SOCKETS_PER_USER = 5` to prevent resource starvation.
