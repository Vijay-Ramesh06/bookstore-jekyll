---
layout: docs
title: "Webhooks"
---

# Webhooks

Webhooks allow you to receive real-time HTTP notifications when events occur in the BookStore system.

## Available Events

| Event | Description |
|---|---|
| `order.created` | A new order was placed |
| `order.confirmed` | An order was confirmed |
| `order.shipped` | An order was dispatched |
| `order.delivered` | An order was delivered |
| `order.cancelled` | An order was cancelled |
| `book.created` | A new book was added |
| `book.updated` | A book's details changed |
| `inventory.low` | A book's stock fell below the reorder level |
| `review.created` | A new review was submitted |

## Registering a Webhook

```bash
curl -X POST https://api.bookstore.example.com/v1/webhooks   -H "Authorization: Bearer YOUR_API_KEY"   -H "Content-Type: application/json"   -d '{
    "url": "https://yourapp.example.com/hooks/bookstore",
    "events": ["order.created", "order.shipped"],
    "secret": "your_webhook_secret"
  }'
```

## Webhook Payload Format

```json
{
  "id": "evt-001",
  "type": "order.created",
  "timestamp": "2025-10-01T12:00:00Z",
  "data": {
    "order": {
      "id": "ord-042",
      "customerId": "cust-001",
      "status": "pending",
      "totalAmount": 42.96
    }
  }
}
```

## Verifying Webhook Signatures

Each webhook request includes a `Bookstore-Signature` header. Always verify it:

```javascript
const crypto = require('crypto');

function verifySignature(rawBody, signature, secret) {
  const computed = crypto
    .createHmac('sha256', secret)
    .update(rawBody)
    .digest('hex');
  return `sha256=${computed}` === signature;
}

app.post('/hooks/bookstore', express.raw({ type: '*/*' }), (req, res) => {
  const sig = req.headers['bookstore-signature'];
  if (!verifySignature(req.body, sig, process.env.WEBHOOK_SECRET)) {
    return res.status(401).send('Invalid signature');
  }
  const event = JSON.parse(req.body);
  console.log(`Event: ${event.type}`);
  res.sendStatus(200);
});
```

## Retry Policy

Failed deliveries (non-2xx responses) are retried up to 5 times with exponential backoff: after 1 minute, 5 minutes, 30 minutes, 2 hours, and 12 hours.

## Managing Webhooks

```bash
# List webhooks
curl https://api.bookstore.example.com/v1/webhooks   -H "Authorization: Bearer YOUR_API_KEY"

# Delete a webhook
curl -X DELETE https://api.bookstore.example.com/v1/webhooks/wh-001   -H "Authorization: Bearer YOUR_API_KEY"
```


