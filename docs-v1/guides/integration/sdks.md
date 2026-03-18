---
layout: docs
version: v1.0
title: "Sdks"
---

# SDKs and Client Libraries

The BookStore API is accessible from any language that can make HTTP requests. Official and community SDKs are available to simplify integration.

## Official SDKs

### JavaScript / TypeScript

```bash
npm install @bookstore/api-client
```

```javascript
import { BookStoreClient } from '@bookstore/api-client';

const client = new BookStoreClient({ apiKey: process.env.BOOKSTORE_API_KEY });

const books = await client.books.list({ category: 'Fiction', inStock: true });
const order = await client.orders.create({
  customerId: 'cust-001',
  items: [{ bookId: 'book-001', quantity: 2 }],
  shippingAddress: { street: '123 Main St', city: 'New York', country: 'US', postalCode: '10001' }
});
```

### Python

```bash
pip install bookstore-api
```

```python
from bookstore import BookStoreClient

client = BookStoreClient(api_key=os.environ['BOOKSTORE_API_KEY'])

books = client.books.list(category='Fiction', in_stock=True)
for book in books:
    print(f"{book.title} Ã¢â‚¬â€ ${book.price}")
```

### PHP

```bash
composer require bookstore/api-client
```

```php
use BookStore\Client;

$client = new Client(['apiKey' => getenv('BOOKSTORE_API_KEY')]);
$books = $client->books()->list(['category' => 'Fiction']);
```

## Generating a Client from OpenAPI

Generate a client in any language using the OpenAPI Generator:

```bash
npm install -g @openapitools/openapi-generator-cli

# Ruby client
openapi-generator-cli generate   -i https://api.bookstore.example.com/v1/openapi.json   -g ruby   -o ./bookstore-ruby-client

# Java client
openapi-generator-cli generate   -i https://api.bookstore.example.com/v1/openapi.json   -g java   -o ./bookstore-java-client
```

## Using Postman

Import the BookStore API collection into Postman:

1. Open Postman
2. Click **Import**
3. Select **Link**
4. Enter: `https://api.bookstore.example.com/v1/openapi.json`
5. Set the `BOOKSTORE_API_KEY` environment variable in Postman

All endpoints are now available with pre-filled request bodies and examples.

## Using cURL

For quick testing without installing any library:

```bash
export BOOKSTORE_API_KEY="your_key_here"
export BASE_URL="https://api.bookstore.example.com/v1"

curl "$BASE_URL/books?category=Fiction"   -H "Authorization: Bearer $BOOKSTORE_API_KEY"
```


