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

The complete endpoint-by-endpoint inventory is cataloged in [`inventories/api-inventory.md`](inventories/api-inventory.md).

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
