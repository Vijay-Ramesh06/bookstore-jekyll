---
layout: docs
title: "Create Review"
---

# Create Review

Submit a customer review for a book.

## Endpoint

```
POST /v1/books/{bookId}/reviews
```

## Path Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `bookId` | string | Yes | Book to review |

## Request Body

```json
{
  "customerId": "cust-001",
  "rating": 5,
  "title": "A timeless classic",
  "body": "One of the greatest American novels ever written. The prose is beautiful and the themes remain highly relevant today."
}
```

## Request Fields

| Field | Type | Required | Description |
|---|---|---|---|
| `customerId` | string | Yes | ID of the reviewing customer |
| `rating` | integer | Yes | Star rating from 1 to 5 |
| `title` | string | No | Short review title (max 100 characters) |
| `body` | string | No | Full review text (max 2000 characters) |

## Review Rules

- A customer can only submit one review per book
- Customers who have purchased the book receive a `verified` badge
- Reviews are published immediately but may be removed if they violate the content policy
- Rating must be an integer between 1 and 5

## Response

```json
{
  "success": true,
  "data": {
    "id": "rev-250",
    "bookId": "book-001",
    "customerId": "cust-001",
    "rating": 5,
    "title": "A timeless classic",
    "verified": true,
    "createdAt": "2025-10-01T12:00:00Z"
  }
}
```

## Error Responses

| Status | Code | Description |
|---|---|---|
| `404` | `RESOURCE_NOT_FOUND` | Book or customer not found |
| `409` | `DUPLICATE_RESOURCE` | Customer has already reviewed this book |
| `422` | `VALIDATION_ERROR` | Rating out of range or body too long |


