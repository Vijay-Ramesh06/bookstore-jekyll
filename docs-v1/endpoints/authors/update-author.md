---
layout: docs
version: v1.0
title: "Update Author"
---

# Update Author

Update an existing author's profile information.

## Endpoint

```
PATCH /v1/authors/{authorId}
```

## Path Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `authorId` | string | Yes | Unique identifier of the author |

## Required Permissions

`read-write` or `admin` API key.

## Request

```bash
curl -X PATCH https://api.bookstore.example.com/v1/authors/auth-025   -H "Authorization: Bearer YOUR_API_KEY"   -H "Content-Type: application/json"   -d '{
    "bio": "Updated biography text.",
    "website": "https://new-website.example.com"
  }'
```

## Updatable Fields

| Field | Type | Description |
|---|---|---|
| `name` | string | Author full name |
| `bio` | string | Author biography |
| `nationality` | string | Country of origin |
| `birthYear` | integer | Year of birth |
| `deathYear` | integer | Year of death |
| `website` | string | Official website URL |

## Response

```json
{
  "success": true,
  "data": {
    "id": "auth-025",
    "name": "George Orwell",
    "bio": "Updated biography text.",
    "updatedAt": "2025-10-01T15:00:00Z"
  }
}
```

## Error Responses

| Status | Code | Description |
|---|---|---|
| `403` | `PERMISSION_DENIED` | Insufficient permissions |
| `404` | `RESOURCE_NOT_FOUND` | Author not found |
| `422` | `VALIDATION_ERROR` | Invalid field values |


