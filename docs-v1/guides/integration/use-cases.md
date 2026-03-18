---
layout: docs
version: v1.0
title: "Use Cases"
---

# Common Use Cases

This guide provides complete examples for the most common BookStore API integration scenarios.

## Use Case 1 Ã¢â‚¬â€ Build a Book Search Page

Fetch books with filtering and display them to users.

```javascript
async function searchBooks(query, category, page = 1) {
  const params = new URLSearchParams({
    search: query,
    page,
    perPage: 20,
    sort: 'averageRating',
    order: 'desc'
  });
  if (category) params.set('category', category);

  const res = await fetch(`${BASE_URL}/books?${params}`, {
    headers: { 'Authorization': `Bearer ${API_KEY}` }
  });
  return res.json();
}

const results = await searchBooks('gatsby', 'Fiction');
results.data.forEach(book => {
  console.log(`${book.title} by ${book.author.name} Ã¢â‚¬â€ $${book.price}`);
});
```

## Use Case 2 Ã¢â‚¬â€ Place an Order

Complete order placement flow with stock checking and error handling.

```javascript
async function placeOrder(customerId, cartItems, shippingAddress) {
  // First check stock for all items
  for (const item of cartItems) {
    const inv = await fetch(`${BASE_URL}/inventory/${item.bookId}`, {
      headers: { 'Authorization': `Bearer ${API_KEY}` }
    }).then(r => r.json());

    if (inv.data.available < item.quantity) {
      throw new Error(`${item.bookId} has only ${inv.data.available} copies available.`);
    }
  }

  // Place the order
  const res = await fetch(`${BASE_URL}/orders`, {
    method: 'POST',
    headers: {
      'Authorization': `Bearer ${API_KEY}`,
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({ customerId, items: cartItems, shippingAddress })
  });

  if (!res.ok) {
    const error = await res.json();
    throw new Error(error.error.message);
  }

  return res.json();
}
```

## Use Case 3 Ã¢â‚¬â€ Inventory Management Dashboard

Monitor and update stock levels.

```python
def get_low_stock_books(threshold=10):
    books = []
    page = 1
    while True:
        response = requests.get(
            f'{BASE_URL}/books',
            params={'page': page, 'perPage': 100},
            headers=headers
        ).json()

        for book in response['data']:
            inv = requests.get(
                f'{BASE_URL}/inventory/{book["id"]}',
                headers=headers
            ).json()
            if inv['data']['available'] < threshold:
                books.append({
                    'id': book['id'],
                    'title': book['title'],
                    'available': inv['data']['available']
                })

        if page >= response['pagination']['totalPages']:
            break
        page += 1

    return sorted(books, key=lambda x: x['available'])

low_stock = get_low_stock_books(threshold=5)
for book in low_stock:
    print(f"LOW STOCK: {book['title']} Ã¢â‚¬â€ {book['available']} remaining")
```

## Use Case 4 Ã¢â‚¬â€ Order Notification System with Webhooks

Receive and process order events in real time.

```javascript
const express = require('express');
const crypto = require('crypto');
const app = express();
app.use(express.json());

app.post('/webhooks/bookstore', (req, res) => {
  // Verify signature
  const sig = req.headers['bookstore-signature'];
  const body = JSON.stringify(req.body);
  const expected = 'sha256=' + crypto
    .createHmac('sha256', process.env.WEBHOOK_SECRET)
    .update(body).digest('hex');

  if (sig !== expected) return res.status(401).send('Invalid signature');

  const { type, data } = req.body;

  switch (type) {
    case 'order.created':
      console.log(`New order ${data.order.id} Ã¢â‚¬â€ $${data.order.totalAmount}`);
      sendConfirmationEmail(data.order);
      break;
    case 'order.shipped':
      console.log(`Order ${data.order.id} shipped Ã¢â‚¬â€ tracking: ${data.order.trackingNumber}`);
      sendShippingNotification(data.order);
      break;
    case 'inventory.low':
      console.log(`Low stock alert: ${data.book.title}`);
      notifyProcurementTeam(data.book);
      break;
  }

  res.sendStatus(200);
});

app.listen(4000);
```


