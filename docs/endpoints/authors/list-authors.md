---
layout: docs
title: "List Authors"
---

# List Authors

Retrieve a paginated list of all authors in the bookstore.

## Endpoint

```
GET /v1/authors
```

## Query Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `page` | integer | No | Page number (default: 1) |
| `perPage` | integer | No | Results per page (default: 20, max: 100) |
| `search` | string | No | Search by author name |
| `nationality` | string | No | Filter by nationality |
| `sort` | string | No | Sort by: `name`, `bookCount`, `createdAt` |
| `order` | string | No | `asc` or `desc` |

## Request

```bash
curl "https://api.bookstore.example.com/v1/authors?search=fitzgerald"   -H "Authorization: Bearer YOUR_API_KEY"
```

## Response

```json
{
  "success": true,
  "data": [
    {
      "id": "auth-001",
      "name": "F. Scott Fitzgerald",
      "nationality": "American",
      "birthYear": 1896,
      "bookCount": 4,
      "createdAt": "2024-01-01T00:00:00Z"
    }
  ],
  "pagination": {
    "total": 340,
    "page": 1,
    "perPage": 20,
    "totalPages": 17
  }
}
```

## Response Fields

| Field | Type | Description |
|---|---|---|
| `id` | string | Unique author identifier |
| `name` | string | Full author name |
| `nationality` | string | Author's nationality |
| `birthYear` | integer | Year of birth |
| `bookCount` | integer | Number of books by this author in the catalog |
| `createdAt` | string | When the author record was created |


