---
layout: docs
version: v1.0
title: "Errors"
---

# Error Reference

The BookStore API uses standard HTTP status codes and returns consistent error responses to help you handle failures gracefully.

## Error Response Format

All error responses follow this structure:

```json
{
  "success": false,
  "error": {
    "code": "RESOURCE_NOT_FOUND",
    "message": "The requested book was not found.",
    "details": {
      "resourceType": "book",
      "resourceId": "book-9999"
    },
    "requestId": "req-abc123"
  }
}
```

## HTTP Status Codes

| Code | Name | Description |
|---|---|---|
| `200` | OK | Request succeeded |
| `201` | Created | Resource created successfully |
| `204` | No Content | Request succeeded, no body returned |
| `400` | Bad Request | Malformed request or invalid parameters |
| `401` | Unauthorized | Missing or invalid API key |
| `403` | Forbidden | Valid key but insufficient permissions |
| `404` | Not Found | Resource does not exist |
| `409` | Conflict | Resource already exists |
| `422` | Unprocessable Entity | Validation error |
| `429` | Too Many Requests | Rate limit exceeded |
| `500` | Internal Server Error | Unexpected server error |
| `503` | Service Unavailable | Server temporarily unavailable |

## Error Codes

| Code | HTTP Status | Description |
|---|---|---|
| `INVALID_API_KEY` | 401 | API key is missing or not recognized |
| `EXPIRED_API_KEY` | 401 | API key has expired |
| `PERMISSION_DENIED` | 403 | Insufficient permissions for this action |
| `RESOURCE_NOT_FOUND` | 404 | Requested resource does not exist |
| `DUPLICATE_RESOURCE` | 409 | Resource with this identifier already exists |
| `VALIDATION_ERROR` | 422 | Request body failed validation |
| `MISSING_REQUIRED_FIELD` | 422 | A required field is missing |
| `INVALID_FIELD_VALUE` | 422 | A field value is invalid |
| `RATE_LIMIT_EXCEEDED` | 429 | Too many requests in the time window |
| `INTERNAL_ERROR` | 500 | Unexpected server-side error |
| `OUT_OF_STOCK` | 422 | Requested quantity exceeds available stock |

## Handling Errors in Code

### JavaScript

```javascript
const response = await fetch('https://api.bookstore.example.com/v1/books/invalid-id', {
  headers: { 'Authorization': `Bearer ${API_KEY}` }
});

if (!response.ok) {
  const error = await response.json();
  console.error(`Error [${error.error.code}]: ${error.error.message}`);
  console.error(`Request ID: ${error.error.requestId}`);
}
```

### Python

```python
response = requests.get(f'{BASE_URL}/books/invalid-id', headers=headers)

if not response.ok:
    error = response.json()['error']
    print(f"Error [{error['code']}]: {error['message']}")
```

## Validation Errors

Validation errors include a `fields` array detailing which fields failed:

```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Request body contains invalid fields.",
    "fields": [
      { "field": "price", "message": "Price must be a positive number." },
      { "field": "isbn", "message": "ISBN must be 13 digits." }
    ]
  }
}
```


