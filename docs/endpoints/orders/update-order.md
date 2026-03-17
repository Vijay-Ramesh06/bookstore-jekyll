---
layout: docs
title: "Update Order"
---

# Update Order

Update the status or shipping details of an existing order.

## Endpoint

```
PATCH /v1/orders/{orderId}
```

## Path Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `orderId` | string | Yes | Unique order identifier |

## Required Permissions

`admin` API key for status changes. `read-write` for notes and address updates on pending orders.

## Updatable Fields

| Field | Allowed When | Description |
|---|---|---|
| `status` | Admin only | Update order status |
| `shippingAddress` | Status is `pending` | Update delivery address |
| `trackingNumber` | Admin only | Add shipment tracking number |
| `notes` | Status is `pending` | Update order notes |

## Status Transition Rules

Valid status transitions:

```
pending â†’ confirmed â†’ shipped â†’ delivered
pending â†’ cancelled
confirmed â†’ cancelled
```

Once an order is `shipped`, `delivered`, or `cancelled`, the status cannot be changed.

## Request

```bash
curl -X PATCH https://api.bookstore.example.com/v1/orders/ord-042   -H "Authorization: Bearer YOUR_API_KEY"   -H "Content-Type: application/json"   -d '{"status": "confirmed", "trackingNumber": "TRK-XYZ789"}'
```

## Response

```json
{
  "success": true,
  "data": {
    "id": "ord-042",
    "status": "confirmed",
    "trackingNumber": "TRK-XYZ789",
    "updatedAt": "2025-10-01T13:00:00Z"
  }
}
```

## Error Responses

| Status | Code | Description |
|---|---|---|
| `403` | `PERMISSION_DENIED` | Insufficient permissions |
| `404` | `RESOURCE_NOT_FOUND` | Order not found |
| `422` | `INVALID_STATUS_TRANSITION` | Invalid status change |


