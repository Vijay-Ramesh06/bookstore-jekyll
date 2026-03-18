---
layout: docs
version: v1.0
title: "Update Book"
---

# Update Book

Update the details of an existing book. Use `PATCH` to update only the fields you provide, or `PUT` to replace the entire book record.

## Endpoints

```
PATCH /v1/books/{bookId}
PUT   /v1/books/{bookId}
```

## Path Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `bookId` | string | Yes | The unique identifier of the book |

## Required Permissions

`read-write` or `admin` API key.

## PATCH Request Ã¢â‚¬â€ Partial Update

Only the fields included in the request body are updated.

```bash
curl -X PATCH https://api.bookstore.example.com/v1/books/book-001   -H "Authorization: Bearer YOUR_API_KEY"   -H "Content-Type: application/json"   -d '{"price": 10.99, "description": "Updated description."}'
```

## PUT Request Ã¢â‚¬â€ Full Replacement

All fields must be provided. Any omitted optional fields are reset to their defaults.

```bash
curl -X PUT https://api.bookstore.example.com/v1/books/book-001   -H "Authorization: Bearer YOUR_API_KEY"   -H "Content-Type: application/json"   -d '{
    "title": "The Great Gatsby",
    "authorId": "auth-001",
    "isbn": "9780743273565",
    "price": 10.99,
    "categoryId": "cat-001"
  }'
```

## Updatable Fields

| Field | Type | Description |
|---|---|---|
| `title` | string | Book title |
| `price` | number | Retail price |
| `description` | string | Book description |
| `categoryId` | string | Category assignment |
| `tags` | array | Descriptive tags |
| `publisher` | string | Publisher name |
| `pages` | integer | Number of pages |

The following fields cannot be updated: `id`, `isbn`, `authorId`, `stock`, `createdAt`.

## Response

```json
{
  "success": true,
  "data": {
    "id": "book-001",
    "title": "The Great Gatsby",
    "price": 10.99,
    "updatedAt": "2025-10-01T14:00:00Z"
  }
}
```

## Error Responses

| Status | Code | Description |
|---|---|---|
| `404` | `RESOURCE_NOT_FOUND` | Book does not exist |
| `422` | `VALIDATION_ERROR` | Invalid field values |


