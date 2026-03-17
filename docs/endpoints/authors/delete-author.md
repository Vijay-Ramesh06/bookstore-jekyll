---
layout: docs
title: "Delete Author"
---

# Delete Author

Permanently remove an author from the database.

## Endpoint

```
DELETE /v1/authors/{authorId}
```

## Required Permissions

`admin` API key.

## Request

```bash
curl -X DELETE https://api.bookstore.example.com/v1/authors/auth-025   -H "Authorization: Bearer YOUR_API_KEY"
```

## Response

`204 No Content` on success.

## Important Notes

- An author cannot be deleted if they have books in the catalog
- First delete or reassign all books by this author before deleting the author record
- Attempting to delete an author with existing books returns a `409 Conflict` error

## Error Responses

| Status | Code | Description |
|---|---|---|
| `403` | `PERMISSION_DENIED` | Only admin keys can delete |
| `404` | `RESOURCE_NOT_FOUND` | Author not found |
| `409` | `CONFLICT` | Author has books in catalog |


