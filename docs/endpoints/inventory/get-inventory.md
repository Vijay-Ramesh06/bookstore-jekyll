---
layout: docs
title: "Get Inventory"
---

# Get Inventory

Retrieve the current stock level and inventory details for a book.

## Endpoint

```
GET /v1/inventory/{bookId}
```

## Path Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `bookId` | string | Yes | Book identifier |

## Request

```bash
curl https://api.bookstore.example.com/v1/inventory/book-001   -H "Authorization: Bearer YOUR_API_KEY"
```

## Response

```json
{
  "success": true,
  "data": {
    "bookId": "book-001",
    "title": "The Great Gatsby",
    "sku": "TGG-001",
    "stock": 42,
    "reserved": 5,
    "available": 37,
    "reorderLevel": 10,
    "reorderQuantity": 50,
    "warehouseLocation": "Section A, Shelf 3",
    "lastRestocked": "2025-09-15T00:00:00Z",
    "lastUpdated": "2025-10-01T09:00:00Z"
  }
}
```

## Response Fields

| Field | Type | Description |
|---|---|---|
| `stock` | integer | Total physical units in warehouse |
| `reserved` | integer | Units reserved for pending orders |
| `available` | integer | Units available for new orders (stock minus reserved) |
| `reorderLevel` | integer | Stock level that triggers a reorder alert |
| `reorderQuantity` | integer | Quantity to order when reorder is triggered |
| `warehouseLocation` | string | Physical location in the warehouse |
| `lastRestocked` | string | Date of the last stock replenishment |

## Error Responses

| Status | Code | Description |
|---|---|---|
| `404` | `RESOURCE_NOT_FOUND` | Book not found |


