---
layout: docs
title: "Create Author"
---

# Create Author

Add a new author to the bookstore database.

## Endpoint

```
POST /v1/authors
```

## Required Permissions

`read-write` or `admin` API key.

## Request Body

```json
{
  "name": "George Orwell",
  "bio": "English novelist and essayist, known for his works on totalitarianism and social inequality.",
  "nationality": "British",
  "birthYear": 1903,
  "deathYear": 1950,
  "website": "https://www.georgeorwell.example.com"
}
```

## Request Fields

| Field | Type | Required | Description |
|---|---|---|---|
| `name` | string | Yes | Full author name (max 100 characters) |
| `bio` | string | No | Author biography (max 2000 characters) |
| `nationality` | string | No | Author's country of origin |
| `birthYear` | integer | No | Year of birth |
| `deathYear` | integer | No | Year of death (null if living) |
| `website` | string | No | Author's official website URL |

## Response

```json
{
  "success": true,
  "data": {
    "id": "auth-025",
    "name": "George Orwell",
    "nationality": "British",
    "birthYear": 1903,
    "bookCount": 0,
    "createdAt": "2025-10-01T12:00:00Z"
  }
}
```

## Error Responses

| Status | Code | Description |
|---|---|---|
| `403` | `PERMISSION_DENIED` | Insufficient permissions |
| `409` | `DUPLICATE_RESOURCE` | Author with this name already exists |
| `422` | `VALIDATION_ERROR` | Invalid field values |


