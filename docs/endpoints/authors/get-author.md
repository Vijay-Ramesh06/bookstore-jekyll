---
layout: docs
title: "Get Author"
---

# Get Author

Retrieve detailed information about a single author including their book list.

## Endpoint

```
GET /v1/authors/{authorId}
```

## Path Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `authorId` | string | Yes | Unique identifier of the author |

## Request

```bash
curl https://api.bookstore.example.com/v1/authors/auth-001   -H "Authorization: Bearer YOUR_API_KEY"
```

## Response

```json
{
  "success": true,
  "data": {
    "id": "auth-001",
    "name": "F. Scott Fitzgerald",
    "bio": "Francis Scott Key Fitzgerald was an American novelist, essayist, and short story writer. He is best known for his novels depicting the flamboyance and excess of the Jazz Age.",
    "nationality": "American",
    "birthYear": 1896,
    "deathYear": 1940,
    "website": "https://www.fscottfitzgerald.example.com",
    "books": [
      {
        "id": "book-001",
        "title": "The Great Gatsby",
        "publishedYear": 1925,
        "price": 12.99
      },
      {
        "id": "book-007",
        "title": "Tender Is the Night",
        "publishedYear": 1934,
        "price": 13.99
      }
    ],
    "bookCount": 4,
    "createdAt": "2024-01-01T00:00:00Z"
  }
}
```

## Error Responses

| Status | Code | Description |
|---|---|---|
| `401` | `INVALID_API_KEY` | API key missing or invalid |
| `404` | `RESOURCE_NOT_FOUND` | Author not found |


