---
layout: docs
version: v1.0
title: "Delete Book"
---

# Delete Book

Permanently remove a book from the catalog. This action cannot be undone.

## Endpoint

```
DELETE /v1/books/{bookId}
```

## Path Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `bookId` | string | Yes | The unique identifier of the book |

## Required Permissions

`admin` API key.

## Request

```bash
curl -X DELETE https://api.bookstore.example.com/v1/books/book-001   -H "Authorization: Bearer YOUR_API_KEY"
```

## Response

On success, the API returns `204 No Content` with an empty response body.

## Important Notes

- Deleting a book removes it from the catalog immediately
- Existing orders that contain this book are not affected Ã¢â‚¬â€ order history is preserved
- Reviews associated with the book are also deleted
- Inventory records for the book are removed
- This action cannot be reversed. Consider updating `stock` to 0 and marking the book as unavailable instead of deleting it

## Soft Delete Alternative

If you want to hide a book without permanently removing it, use the archive endpoint instead:

```bash
curl -X POST https://api.bookstore.example.com/v1/books/book-001/archive   -H "Authorization: Bearer YOUR_API_KEY"
```

Archived books are hidden from public listings but remain in the database. They can be restored later.

## Error Responses

| Status | Code | Description |
|---|---|---|
| `401` | `INVALID_API_KEY` | API key missing or invalid |
| `403` | `PERMISSION_DENIED` | Only admin keys can delete books |
| `404` | `RESOURCE_NOT_FOUND` | Book does not exist |


