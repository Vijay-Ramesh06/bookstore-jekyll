---
layout: docs
version: v1.0
title: "Update Inventory"
---

# Update Inventory

Update the stock level and inventory settings for a book.

## Endpoint

```
PATCH /v1/inventory/{bookId}
```

## Required Permissions

`admin` API key.

## Request Body

```json
{
  "stock": 100,
  "reorderLevel": 15,
  "reorderQuantity": 75,
  "warehouseLocation": "Section B, Shelf 1",
  "notes": "Restocked from supplier order #PO-2025-089"
}
```

## Request Fields

| Field | Type | Required | Description |
|---|---|---|---|
| `stock` | integer | No | Set absolute stock level |
| `adjustment` | integer | No | Add or subtract from current stock (positive or negative) |
| `reorderLevel` | integer | No | Minimum stock before reorder alert |
| `reorderQuantity` | integer | No | Quantity to reorder |
| `warehouseLocation` | string | No | Physical warehouse location |
| `notes` | string | No | Reason for stock change (for audit log) |

Use either `stock` (absolute) or `adjustment` (relative), not both.

## Examples

### Set absolute stock level

```bash
curl -X PATCH https://api.bookstore.example.com/v1/inventory/book-001   -H "Authorization: Bearer YOUR_API_KEY"   -H "Content-Type: application/json"   -d '{"stock": 100, "notes": "Initial stock entry"}'
```

### Adjust stock by a relative amount

```bash
curl -X PATCH https://api.bookstore.example.com/v1/inventory/book-001   -H "Authorization: Bearer YOUR_API_KEY"   -H "Content-Type: application/json"   -d '{"adjustment": -5, "notes": "Damaged items removed from stock"}'
```

## Response

```json
{
  "success": true,
  "data": {
    "bookId": "book-001",
    "stock": 100,
    "available": 95,
    "lastUpdated": "2025-10-01T12:00:00Z"
  }
}
```

## Error Responses

| Status | Code | Description |
|---|---|---|
| `403` | `PERMISSION_DENIED` | Only admin keys can update inventory |
| `404` | `RESOURCE_NOT_FOUND` | Book not found |
| `422` | `VALIDATION_ERROR` | Both stock and adjustment provided, or stock would go below zero |


