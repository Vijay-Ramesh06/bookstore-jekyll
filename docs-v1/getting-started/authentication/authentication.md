---
layout: docs
version: v1.0
title: "Authentication"
---

# Authentication

The BookStore API uses API key authentication. Every request must include a valid API key in the `Authorization` header.

## Generating an API Key

1. Log in to the BookStore developer portal at `https://developers.bookstore.example.com`
2. Navigate to **Account Ã¢â€ â€™ API Keys**
3. Click **Generate New Key**
4. Give the key a name (for example, `my-app-production`)
5. Copy the key immediately Ã¢â‚¬â€ it is shown only once

## Using Your API Key

Include the key in every request using the `Authorization` header:

```
Authorization: Bearer YOUR_API_KEY
```

### Example Request

```bash
curl https://api.bookstore.example.com/v1/books   -H "Authorization: Bearer YOUR_API_KEY"
```

### Example with JavaScript

```javascript
const response = await fetch('https://api.bookstore.example.com/v1/books', {
  headers: {
    'Authorization': `Bearer ${process.env.BOOKSTORE_API_KEY}`,
    'Content-Type': 'application/json'
  }
});
const data = await response.json();
```

### Example with Python

```python
import requests

headers = {
    'Authorization': f'Bearer {API_KEY}',
    'Content-Type': 'application/json'
}

response = requests.get('https://api.bookstore.example.com/v1/books', headers=headers)
data = response.json()
```

## API Key Types

| Type | Description |
|---|---|
| `read-only` | Can only perform GET requests |
| `read-write` | Can perform all request types |
| `admin` | Full access including delete and user management |

## API Key Security Best Practices

- Store your API key in environment variables, never in source code
- Use separate keys for development, staging, and production environments
- Set an expiry date when creating keys for temporary access
- Revoke unused keys immediately from the developer portal
- Never log or expose your API key in client-side code

## Revoking an API Key

To revoke a key, go to **Account Ã¢â€ â€™ API Keys** in the developer portal and click **Revoke** next to the key. Revoked keys are invalidated immediately.

## Error Responses for Authentication

| Status | Meaning |
|---|---|
| `401 Unauthorized` | API key is missing or invalid |
| `403 Forbidden` | API key is valid but lacks permission for this action |


