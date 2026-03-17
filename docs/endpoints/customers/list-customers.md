---
layout: docs
title: "List Customers"
---

# List Customers

Retrieve a paginated list of registered customers.

## Endpoint

```
GET /v1/customers
```

## Required Permissions

`admin` API key. Customer data is sensitive and restricted to admin access.

## Query Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `page` | integer | No | Page number (default: 1) |
| `perPage` | integer | No | Results per page (default: 20) |
| `search` | string | No | Search by name or email |
| `sort` | string | No | Sort by `name`, `email`, `createdAt` |
| `order` | string | No | `asc` or `desc` |

## Request

```bash
curl "https://api.bookstore.example.com/v1/customers?search=alice"   -H "Authorization: Bearer YOUR_API_KEY"
```

## Response

```json
{
  "success": true,
  "data": [
    {
      "id": "cust-001",
      "name": "Alice Smith",
      "email": "alice@example.com",
      "orderCount": 12,
      "totalSpent": 189.45,
      "createdAt": "2024-03-15T00:00:00Z"
    }
  ],
  "pagination": {
    "total": 5230,
    "page": 1,
    "perPage": 20,
    "totalPages": 262
  }
}
```


