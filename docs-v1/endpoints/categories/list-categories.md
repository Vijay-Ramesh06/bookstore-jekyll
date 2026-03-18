---
layout: docs
version: v1.0
title: "List Categories"
---

# List Categories

Retrieve all book categories available in the store.

## Endpoint

```
GET /v1/categories
```

## Request

```bash
curl https://api.bookstore.example.com/v1/categories   -H "Authorization: Bearer YOUR_API_KEY"
```

## Response

```json
{
  "success": true,
  "data": [
    {
      "id": "cat-001",
      "name": "Fiction",
      "slug": "fiction",
      "description": "Novels and short stories of imagined events.",
      "bookCount": 420
    },
    {
      "id": "cat-002",
      "name": "Non-Fiction",
      "slug": "non-fiction",
      "description": "Books based on real events and factual information.",
      "bookCount": 315
    },
    {
      "id": "cat-003",
      "name": "Science Fiction",
      "slug": "science-fiction",
      "description": "Speculative fiction based on science and technology.",
      "bookCount": 188
    },
    {
      "id": "cat-004",
      "name": "Mystery",
      "slug": "mystery",
      "description": "Stories involving crime, investigation, and suspense.",
      "bookCount": 240
    },
    {
      "id": "cat-005",
      "name": "Biography",
      "slug": "biography",
      "description": "Life stories of real individuals.",
      "bookCount": 97
    }
  ],
  "pagination": {
    "total": 18,
    "page": 1,
    "perPage": 20,
    "totalPages": 1
  }
}
```

Categories are relatively static. Consider caching this response for up to 1 hour to reduce unnecessary API calls.


