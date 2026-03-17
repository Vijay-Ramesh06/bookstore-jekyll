---
layout: docs
title: "Get Book"
---

# Get Book

Retrieve detailed information about a single book by its ID.

## Endpoint

```
GET /v1/books/{bookId}
```

## Path Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `bookId` | string | Yes | The unique identifier of the book |

## Request

```bash
curl https://api.bookstore.example.com/v1/books/book-001   -H "Authorization: Bearer YOUR_API_KEY"
```

## Response

```json
{
  "success": true,
  "data": {
    "id": "book-001",
    "title": "The Great Gatsby",
    "author": {
      "id": "auth-001",
      "name": "F. Scott Fitzgerald",
      "bio": "American novelist and short story writer."
    },
    "isbn": "9780743273565",
    "price": 12.99,
    "category": {
      "id": "cat-001",
      "name": "Fiction"
    },
    "description": "A novel set in the Jazz Age on Long Island, depicting the mysterious millionaire Jay Gatsby and his obsession with the beautiful Daisy Buchanan.",
    "publishedYear": 1925,
    "publisher": "Scribner",
    "language": "English",
    "pages": 180,
    "stock": 42,
    "averageRating": 4.2,
    "reviewCount": 128,
    "tags": ["classic", "american-literature", "jazz-age"],
    "createdAt": "2024-01-01T00:00:00Z",
    "updatedAt": "2025-01-15T10:30:00Z"
  }
}
```

## Response Fields

| Field | Type | Description |
|---|---|---|
| `id` | string | Unique book identifier |
| `title` | string | Full book title |
| `author` | object | Author details including bio |
| `isbn` | string | 13-digit ISBN number |
| `price` | number | Current retail price in USD |
| `category` | object | Book category details |
| `description` | string | Full book description |
| `publishedYear` | integer | Year of original publication |
| `publisher` | string | Publishing house name |
| `language` | string | Language of the book |
| `pages` | integer | Total number of pages |
| `stock` | integer | Current quantity in stock |
| `averageRating` | number | Mean rating from all reviews |
| `reviewCount` | integer | Total number of submitted reviews |
| `tags` | array | Descriptive tags for the book |

## Error Responses

| Status | Code | Description |
|---|---|---|
| `401` | `INVALID_API_KEY` | API key missing or invalid |
| `404` | `RESOURCE_NOT_FOUND` | Book with given ID does not exist |


