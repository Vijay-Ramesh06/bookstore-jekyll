---
layout: docs
title: "Status Codes"
---

# Status Codes and Headers

This page is a complete reference for HTTP status codes, response headers, and error codes used by the BookStore API.

## HTTP Status Codes

### Success Codes

| Code | Name | When Used |
|---|---|---|
| `200 OK` | Success | Successful `GET`, `PATCH`, `PUT` requests |
| `201 Created` | Created | Successful `POST` requests that create resources |
| `204 No Content` | No Content | Successful `DELETE` requests |

### Client Error Codes

| Code | Name | Common Causes |
|---|---|---|
| `400 Bad Request` | Bad Request | Malformed JSON, missing required headers |
| `401 Unauthorized` | Unauthorized | Missing, invalid, or expired API key |
| `403 Forbidden` | Forbidden | Valid key but insufficient permissions |
| `404 Not Found` | Not Found | Resource ID does not exist |
| `405 Method Not Allowed` | Method Not Allowed | Using wrong HTTP method on endpoint |
| `409 Conflict` | Conflict | Duplicate ISBN, email already registered |
| `422 Unprocessable Entity` | Validation Error | Invalid field values, out of stock |
| `429 Too Many Requests` | Rate Limited | Exceeded rate limit for your plan |

### Server Error Codes

| Code | Name | Action |
|---|---|---|
| `500 Internal Server Error` | Server Error | Retry after a delay; contact support if persistent |
| `503 Service Unavailable` | Unavailable | Temporary outage; check status page |

## Standard Response Headers

| Header | Description |
|---|---|
| `Content-Type` | Always `application/json` |
| `X-Request-Id` | Unique identifier for this request |
| `X-RateLimit-Limit` | Rate limit ceiling |
| `X-RateLimit-Remaining` | Requests left in current window |
| `X-RateLimit-Reset` | Unix timestamp when limit resets |
| `Retry-After` | Seconds to wait (429 responses only) |
| `Bookstore-Api-Version` | API version used for this request |

## Application Error Codes

| Code | Status | Description |
|---|---|---|
| `INVALID_API_KEY` | 401 | API key not recognized |
| `EXPIRED_API_KEY` | 401 | API key has passed expiry date |
| `PERMISSION_DENIED` | 403 | Key lacks required permission |
| `RESOURCE_NOT_FOUND` | 404 | Requested resource does not exist |
| `DUPLICATE_RESOURCE` | 409 | Unique constraint violation |
| `VALIDATION_ERROR` | 422 | One or more fields failed validation |
| `MISSING_REQUIRED_FIELD` | 422 | Required field not provided |
| `INVALID_FIELD_VALUE` | 422 | Field value out of range or wrong format |
| `OUT_OF_STOCK` | 422 | Requested quantity not available |
| `CANNOT_CANCEL` | 422 | Order in non-cancellable state |
| `INVALID_STATUS_TRANSITION` | 422 | Invalid order status change |
| `RATE_LIMIT_EXCEEDED` | 429 | Rate limit reached |
| `INTERNAL_ERROR` | 500 | Unexpected server error |


