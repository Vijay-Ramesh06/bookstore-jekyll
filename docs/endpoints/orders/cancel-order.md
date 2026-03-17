---
layout: docs
title: "Cancel Order"
---

# Cancel Order

Cancel an existing order. Orders can only be cancelled if they have not yet been shipped.

## Endpoint

```
POST /v1/orders/{orderId}/cancel
```

## Path Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `orderId` | string | Yes | Unique order identifier |

## Request Body

```json
{
  "reason": "Customer requested cancellation."
}
```

| Field | Type | Required | Description |
|---|---|---|---|
| `reason` | string | No | Reason for cancellation (max 500 characters) |

## Request

```bash
curl -X POST https://api.bookstore.example.com/v1/orders/ord-042/cancel   -H "Authorization: Bearer YOUR_API_KEY"   -H "Content-Type: application/json"   -d '{"reason": "Customer requested cancellation."}'
```

## Response

```json
{
  "success": true,
  "data": {
    "id": "ord-042",
    "status": "cancelled",
    "cancelledAt": "2025-10-01T14:00:00Z",
    "reason": "Customer requested cancellation."
  }
}
```

## Stock Restoration

When an order is cancelled, the stock levels for all items in the order are automatically restored.

## Refund Policy

Cancellations of `pending` orders are refunded immediately. Cancellations of `confirmed` orders may take 3â€“5 business days to process the refund.

## Error Responses

| Status | Code | Description |
|---|---|---|
| `404` | `RESOURCE_NOT_FOUND` | Order not found |
| `422` | `CANNOT_CANCEL` | Order has already been shipped or delivered |


