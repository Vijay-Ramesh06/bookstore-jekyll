---
layout: docs
version: v1.0
title: "Create Category"
---

# Create Category

Add a new book category to the store.

## Endpoint

```
POST /v1/categories
```

## Required Permissions

`admin` API key.

## Request Body

```json
{
  "name": "Graphic Novels",
  "description": "Books that combine text and sequential art to tell a story.",
  "slug": "graphic-novels"
}
```

## Request Fields

| Field | Type | Required | Description |
|---|---|---|---|
| `name` | string | Yes | Category display name (max 50 characters) |
| `description` | string | No | Short description of the category |
| `slug` | string | No | URL-friendly identifier. Auto-generated from name if not provided |

## Response

```json
{
  "success": true,
  "data": {
    "id": "cat-019",
    "name": "Graphic Novels",
    "slug": "graphic-novels",
    "description": "Books that combine text and sequential art to tell a story.",
    "bookCount": 0,
    "createdAt": "2025-10-01T12:00:00Z"
  }
}
```

## Error Responses

| Status | Code | Description |
|---|---|---|
| `403` | `PERMISSION_DENIED` | Only admin keys can create categories |
| `409` | `DUPLICATE_RESOURCE` | Category name or slug already exists |
| `422` | `VALIDATION_ERROR` | Invalid field values |


