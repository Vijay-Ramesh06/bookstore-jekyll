---
layout: docs
version: v1.0
title: "Get Category"
---

# Get Category

Retrieve details and the list of books for a specific category.

## Endpoint

```
GET /v1/categories/{categoryId}
```

## Path Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `categoryId` | string | Yes | Category ID or slug |

## Request

```bash
curl https://api.bookstore.example.com/v1/categories/fiction   -H "Authorization: Bearer YOUR_API_KEY"
```

You can use either the category `id` (e.g., `cat-001`) or the `slug` (e.g., `fiction`) in the URL.

## Response

```json
{
  "success": true,
  "data": {
    "id": "cat-001",
    "name": "Fiction",
    "slug": "fiction",
    "description": "Novels and short stories of imagined events.",
    "bookCount": 420,
    "books": [
      {
        "id": "book-001",
        "title": "The Great Gatsby",
        "author": { "id": "auth-001", "name": "F. Scott Fitzgerald" },
        "price": 12.99,
        "stock": 42
      }
    ]
  },
  "pagination": {
    "total": 420,
    "page": 1,
    "perPage": 20,
    "totalPages": 21
  }
}
```

## Error Responses

| Status | Code | Description |
|---|---|---|
| `404` | `RESOURCE_NOT_FOUND` | Category not found |


