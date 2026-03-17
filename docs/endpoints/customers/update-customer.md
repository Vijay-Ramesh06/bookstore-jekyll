---
layout: docs
title: "Update Customer"
---

# Update Customer

Update a customer's profile information.

## Endpoint

```
PATCH /v1/customers/{customerId}
```

## Required Permissions

`admin` API key, or the customer's own session token.

## Request

```bash
curl -X PATCH https://api.bookstore.example.com/v1/customers/cust-001   -H "Authorization: Bearer YOUR_API_KEY"   -H "Content-Type: application/json"   -d '{"phone": "+1-555-9999", "name": "Alice Johnson"}'
```

## Updatable Fields

| Field | Type | Description |
|---|---|---|
| `name` | string | Customer full name |
| `phone` | string | Phone number |
| `email` | string | Email address (requires verification) |

Note: Email changes require the customer to verify the new address before it takes effect.

## Response

```json
{
  "success": true,
  "data": {
    "id": "cust-001",
    "name": "Alice Johnson",
    "phone": "+1-555-9999",
    "updatedAt": "2025-10-01T16:00:00Z"
  }
}
```


