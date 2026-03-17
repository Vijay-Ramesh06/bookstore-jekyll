---
layout: docs
title: "Rate Limiting"
---

# Rate Limiting

The BookStore API enforces rate limits to ensure fair usage and platform reliability.

## Rate Limit Tiers

| Plan | Requests per Minute | Requests per Day |
|---|---|---|
| Free | 60 | 1,000 |
| Developer | 300 | 10,000 |
| Business | 1,000 | 100,000 |
| Enterprise | Custom | Custom |

Rate limits are applied per API key.

## Rate Limit Headers

Every API response includes these headers:

| Header | Description |
|---|---|
| `X-RateLimit-Limit` | Maximum requests allowed per minute |
| `X-RateLimit-Remaining` | Requests remaining in the current window |
| `X-RateLimit-Reset` | Unix timestamp when the window resets |
| `Retry-After` | Seconds to wait before retrying (only on 429 responses) |

## Handling 429 Responses

When you exceed the rate limit, the API returns a `429 Too Many Requests` response:

```json
{
  "success": false,
  "error": {
    "code": "RATE_LIMIT_EXCEEDED",
    "message": "Rate limit exceeded. Please wait before making more requests.",
    "retryAfter": 30
  }
}
```

Handle this in your code:

```javascript
async function apiRequest(url, options, retries = 3) {
  const response = await fetch(url, options);

  if (response.status === 429) {
    const retryAfter = parseInt(response.headers.get('Retry-After') || '60');
    console.log(`Rate limited. Waiting ${retryAfter} seconds...`);
    await new Promise(r => setTimeout(r, retryAfter * 1000));
    return retries > 0 ? apiRequest(url, options, retries - 1) : response;
  }

  return response;
}
```

## Best Practices to Avoid Rate Limiting

- Cache responses that do not change frequently, such as category lists
- Use pagination instead of requesting all records at once
- Use the `fields` query parameter to request only the data you need
- Implement exponential backoff for retries
- Use webhooks for real-time updates instead of polling

## Checking Your Current Usage

```bash
curl -I https://api.bookstore.example.com/v1/books   -H "Authorization: Bearer YOUR_API_KEY"
```

Check the `X-RateLimit-Remaining` header in the response.


