---
layout: docs
title: "List Orders"
---

# List Orders

Retrieve a paginated list of customer orders.

## Endpoint

```
GET /v1/orders
```

## Query Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `page` | integer | No | Page number (default: 1) |
| `perPage` | integer | No | Results per page (default: 20) |
| `customerId` | string | No | Filter by customer |
| `status` | string | No | Filter by order status |
| `fromDate` | string | No | Orders created after this date (ISO 8601) |
| `toDate` | string | No | Orders created before this date (ISO 8601) |
| `sort` | string | No | Sort by: `createdAt`, `totalAmount` |
| `order` | string | No | `asc` or `desc` |

## Order Statuses

| Status | Description |
|---|---|
| `pending` | Order placed, awaiting confirmation |
| `confirmed` | Order confirmed, preparing for shipment |
| `shipped` | Order dispatched from warehouse |
| `delivered` | Order received by customer |
| `cancelled` | Order cancelled |
| `refunded` | Order refunded |

## Request

```bash
curl "https://api.bookstore.example.com/v1/orders?status=pending&sort=createdAt&order=desc"   -H "Authorization: Bearer YOUR_API_KEY"
```

## Response

```json
{
  "success": true,
  "data": [
    {
      "id": "ord-001",
      "customer": { "id": "cust-001", "name": "Alice Smith" },
      "status": "confirmed",
      "totalAmount": 37.97,
      "itemCount": 3,
      "createdAt": "2025-10-01T09:00:00Z"
    }
  ],
  "pagination": {
    "total": 8420,
    "page": 1,
    "perPage": 20,
    "totalPages": 421
  }
}
```


