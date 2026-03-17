---
layout: docs
title: "Delete Review"
---

# Delete Review

Remove a customer review from a book.

## Endpoint

```
DELETE /v1/books/{bookId}/reviews/{reviewId}
```

## Path Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `bookId` | string | Yes | Book identifier |
| `reviewId` | string | Yes | Review identifier |

## Required Permissions

`admin` API key, or the review author's own session token.

## Request

```bash
curl -X DELETE   https://api.bookstore.example.com/v1/books/book-001/reviews/rev-001   -H "Authorization: Bearer YOUR_API_KEY"
```

## Response

`204 No Content` on success.

## Effects

When a review is deleted:
- The book's `averageRating` and `reviewCount` are recalculated automatically
- The action is logged in the audit trail
- The customer is notified by email if the deletion was performed by an admin

## Error Responses

| Status | Code | Description |
|---|---|---|
| `403` | `PERMISSION_DENIED` | Attempting to delete another user's review |
| `404` | `RESOURCE_NOT_FOUND` | Review or book not found |


