---
layout: docs
version: v1.0
title: "Create Book"
---

# Create Book

Add a new book to the bookstore catalog.

## Endpoint

```
POST /v1/books
```

## Required Permissions

`read-write` or `admin` API key.

## Request Body

```json
{
  "title": "To Kill a Mockingbird",
  "authorId": "auth-002",
  "isbn": "9780061935466",
  "price": 14.99,
  "categoryId": "cat-001",
  "description": "A novel about racial injustice and moral growth in the American South.",
  "publishedYear": 1960,
  "publisher": "J.B. Lippincott & Co.",
  "language": "English",
  "pages": 281,
  "tags": ["classic", "american-literature", "legal-drama"]
}
```

## Request Fields

| Field | Type | Required | Description |
|---|---|---|---|
| `title` | string | Yes | Book title (max 255 characters) |
| `authorId` | string | Yes | ID of an existing author |
| `isbn` | string | Yes | Unique 13-digit ISBN |
| `price` | number | Yes | Retail price, must be greater than 0 |
| `categoryId` | string | Yes | ID of an existing category |
| `description` | string | No | Book description (max 2000 characters) |
| `publishedYear` | integer | No | Year of publication |
| `publisher` | string | No | Publisher name |
| `language` | string | No | Language (default: `English`) |
| `pages` | integer | No | Number of pages |
| `tags` | array | No | List of descriptive string tags |

## Response

```json
{
  "success": true,
  "data": {
    "id": "book-025",
    "title": "To Kill a Mockingbird",
    "authorId": "auth-002",
    "isbn": "9780061935466",
    "price": 14.99,
    "categoryId": "cat-001",
    "stock": 0,
    "createdAt": "2025-10-01T12:00:00Z"
  }
}
```

A newly created book has a `stock` of 0 by default. Use the [Update Inventory](../inventory/update-inventory.md) endpoint to add stock.

## Error Responses

| Status | Code | Description |
|---|---|---|
| `401` | `INVALID_API_KEY` | API key missing or invalid |
| `403` | `PERMISSION_DENIED` | Read-only key cannot create resources |
| `409` | `DUPLICATE_RESOURCE` | A book with this ISBN already exists |
| `422` | `VALIDATION_ERROR` | Request body failed validation |
| `422` | `MISSING_REQUIRED_FIELD` | A required field is missing |


