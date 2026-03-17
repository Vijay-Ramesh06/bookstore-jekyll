---
layout: docs
title: "List Reviews"
---

# List Reviews

Retrieve customer reviews for a specific book.

## Endpoint

```
GET /v1/books/{bookId}/reviews
```

## Path Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `bookId` | string | Yes | Book identifier |

## Query Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `page` | integer | No | Page number (default: 1) |
| `perPage` | integer | No | Results per page (default: 10) |
| `sort` | string | No | Sort by: `createdAt`, `rating` |
| `order` | string | No | `asc` or `desc` (default: `desc`) |
| `rating` | integer | No | Filter by star rating (1â€“5) |

## Request

```bash
curl "https://api.bookstore.example.com/v1/books/book-001/reviews?sort=rating&order=desc"   -H "Authorization: Bearer YOUR_API_KEY"
```

## Response

```json
{
  "success": true,
  "data": [
    {
      "id": "rev-001",
      "customer": { "id": "cust-001", "name": "Alice S." },
      "rating": 5,
      "title": "A timeless classic",
      "body": "One of the greatest American novels ever written. The prose is beautiful and the themes remain relevant today.",
      "verified": true,
      "createdAt": "2025-09-01T10:00:00Z"
    }
  ],
  "summary": {
    "averageRating": 4.2,
    "totalReviews": 128,
    "distribution": {
      "5": 68,
      "4": 32,
      "3": 15,
      "2": 8,
      "1": 5
    }
  },
  "pagination": {
    "total": 128,
    "page": 1,
    "perPage": 10,
    "totalPages": 13
  }
}
```

The `verified` field indicates whether the reviewer purchased the book through the BookStore.


