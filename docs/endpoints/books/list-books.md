---
layout: docs
title: "List Books"
---

# List Books

Retrieve a paginated list of all books in the store.

## Endpoint

```
GET /v1/books
```

## Query Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `page` | integer | No | Page number (default: 1) |
| `perPage` | integer | No | Results per page (default: 20, max: 100) |
| `search` | string | No | Search by title, author, or ISBN |
| `category` | string | No | Filter by category ID or name |
| `authorId` | string | No | Filter by author ID |
| `minPrice` | number | No | Minimum price filter |
| `maxPrice` | number | No | Maximum price filter |
| `inStock` | boolean | No | Filter to in-stock books only |
| `sort` | string | No | Sort field: `title`, `price`, `publishedYear`, `createdAt` |
| `order` | string | No | Sort order: `asc` or `desc` |

## Request

```bash
curl "https://api.bookstore.example.com/v1/books?category=Fiction&inStock=true&sort=price&order=asc"   -H "Authorization: Bearer YOUR_API_KEY"
```

## Response

```json
{
  "success": true,
  "data": [
    {
      "id": "book-001",
      "title": "The Great Gatsby",
      "author": {
        "id": "auth-001",
        "name": "F. Scott Fitzgerald"
      },
      "isbn": "9780743273565",
      "price": 12.99,
      "category": {
        "id": "cat-001",
        "name": "Fiction"
      },
      "publishedYear": 1925,
      "stock": 42,
      "averageRating": 4.2,
      "reviewCount": 128,
      "createdAt": "2024-01-01T00:00:00Z"
    }
  ],
  "pagination": {
    "total": 1250,
    "page": 1,
    "perPage": 20,
    "totalPages": 63
  }
}
```

## Response Fields

| Field | Type | Description |
|---|---|---|
| `id` | string | Unique book identifier |
| `title` | string | Book title |
| `author` | object | Author name and ID |
| `isbn` | string | 13-digit ISBN |
| `price` | number | Current price in USD |
| `category` | object | Category name and ID |
| `publishedYear` | integer | Year of publication |
| `stock` | integer | Current stock level |
| `averageRating` | number | Average customer rating (1â€“5) |
| `reviewCount` | integer | Total number of reviews |

## Error Responses

| Status | Code | Description |
|---|---|---|
| `401` | `INVALID_API_KEY` | API key missing or invalid |
| `422` | `INVALID_FIELD_VALUE` | Invalid query parameter value |

Last reviewed: October 2025.

