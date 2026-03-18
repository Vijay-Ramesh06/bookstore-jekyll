---
layout: docs
version: v1.0
title: "Create Order"
---

# Create Order

Place a new order for one or more books.

## Endpoint

```
POST /v1/orders
```

## Request Body

```json
{
  "customerId": "cust-001",
  "items": [
    { "bookId": "book-001", "quantity": 2 },
    { "bookId": "book-002", "quantity": 1 }
  ],
  "shippingAddress": {
    "street": "123 Main St",
    "city": "New York",
    "state": "NY",
    "country": "US",
    "postalCode": "10001"
  },
  "notes": "Please gift wrap the items."
}
```

## Request Fields

| Field | Type | Required | Description |
|---|---|---|---|
| `customerId` | string | Yes | ID of the customer placing the order |
| `items` | array | Yes | List of books and quantities (min 1 item) |
| `items[].bookId` | string | Yes | Book identifier |
| `items[].quantity` | integer | Yes | Quantity (min 1) |
| `shippingAddress` | object | Yes | Delivery address |
| `shippingAddress.street` | string | Yes | Street address |
| `shippingAddress.city` | string | Yes | City |
| `shippingAddress.country` | string | Yes | ISO 3166-1 country code |
| `shippingAddress.postalCode` | string | Yes | Postal or ZIP code |
| `notes` | string | No | Special instructions |

## Response

```json
{
  "success": true,
  "data": {
    "id": "ord-042",
    "status": "pending",
    "totalAmount": 42.96,
    "estimatedDelivery": "2025-10-07",
    "createdAt": "2025-10-01T12:00:00Z"
  }
}
```

## Stock Validation

The API validates stock availability for each item before creating the order. If any item is out of stock, the entire order is rejected with a `422` error and a list of unavailable items.

## Error Responses

| Status | Code | Description |
|---|---|---|
| `404` | `RESOURCE_NOT_FOUND` | Customer or book not found |
| `422` | `OUT_OF_STOCK` | One or more items are out of stock |
| `422` | `VALIDATION_ERROR` | Invalid request body |


