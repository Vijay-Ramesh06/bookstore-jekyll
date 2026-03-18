---
layout: docs
version: v1.0
title: "Get Customer"
---

# Get Customer

Retrieve full profile and order history for a single customer.

## Endpoint

```
GET /v1/customers/{customerId}
```

## Required Permissions

`admin` API key.

## Request

```bash
curl https://api.bookstore.example.com/v1/customers/cust-001   -H "Authorization: Bearer YOUR_API_KEY"
```

## Response

```json
{
  "success": true,
  "data": {
    "id": "cust-001",
    "name": "Alice Smith",
    "email": "alice@example.com",
    "phone": "+1-555-0100",
    "addresses": [
      {
        "id": "addr-001",
        "label": "Home",
        "street": "123 Main St",
        "city": "New York",
        "country": "US",
        "postalCode": "10001",
        "isDefault": true
      }
    ],
    "orderCount": 12,
    "totalSpent": 189.45,
    "lastOrderDate": "2025-09-20T00:00:00Z",
    "createdAt": "2024-03-15T00:00:00Z"
  }
}
```

## Error Responses

| Status | Code | Description |
|---|---|---|
| `403` | `PERMISSION_DENIED` | Non-admin access attempted |
| `404` | `RESOURCE_NOT_FOUND` | Customer not found |


