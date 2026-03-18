---
layout: docs
version: v1.0
title: "Create Customer"
---

# Create Customer

Register a new customer account.

## Endpoint

```
POST /v1/customers
```

## Request Body

```json
{
  "name": "Bob Johnson",
  "email": "bob@example.com",
  "phone": "+1-555-0200",
  "address": {
    "street": "456 Oak Ave",
    "city": "Los Angeles",
    "state": "CA",
    "country": "US",
    "postalCode": "90001"
  }
}
```

## Request Fields

| Field | Type | Required | Description |
|---|---|---|---|
| `name` | string | Yes | Full name (max 100 characters) |
| `email` | string | Yes | Valid unique email address |
| `phone` | string | No | Phone number in E.164 format |
| `address` | object | No | Default shipping address |

## Response

```json
{
  "success": true,
  "data": {
    "id": "cust-125",
    "name": "Bob Johnson",
    "email": "bob@example.com",
    "orderCount": 0,
    "createdAt": "2025-10-01T12:00:00Z"
  }
}
```

## Error Responses

| Status | Code | Description |
|---|---|---|
| `409` | `DUPLICATE_RESOURCE` | Email already registered |
| `422` | `VALIDATION_ERROR` | Invalid fields |


