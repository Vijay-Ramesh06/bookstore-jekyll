---
layout: docs
version: v1.0
title: "Get Order"
---

# Get Order

Retrieve the full details of a single order including all items and shipping information.

## Endpoint

```
GET /v1/orders/{orderId}
```

## Path Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `orderId` | string | Yes | Unique order identifier |

## Request

```bash
curl https://api.bookstore.example.com/v1/orders/ord-001   -H "Authorization: Bearer YOUR_API_KEY"
```

## Response

```json
{
  "success": true,
  "data": {
    "id": "ord-001",
    "customer": {
      "id": "cust-001",
      "name": "Alice Smith",
      "email": "alice@example.com"
    },
    "status": "confirmed",
    "items": [
      {
        "book": { "id": "book-001", "title": "The Great Gatsby" },
        "quantity": 2,
        "unitPrice": 12.99,
        "subtotal": 25.98
      },
      {
        "book": { "id": "book-002", "title": "1984" },
        "quantity": 1,
        "unitPrice": 11.99,
        "subtotal": 11.99
      }
    ],
    "subtotal": 37.97,
    "shippingCost": 4.99,
    "totalAmount": 42.96,
    "shippingAddress": {
      "street": "123 Main St",
      "city": "New York",
      "state": "NY",
      "country": "US",
      "postalCode": "10001"
    },
    "trackingNumber": "TRK-ABC123456",
    "createdAt": "2025-10-01T09:00:00Z",
    "updatedAt": "2025-10-01T10:30:00Z"
  }
}
```

## Error Responses

| Status | Code | Description |
|---|---|---|
| `404` | `RESOURCE_NOT_FOUND` | Order not found |


