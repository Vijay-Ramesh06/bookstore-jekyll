---
layout: docs
title: "Quickstart"
---

# Quickstart

This guide gets you up and running with the BookStore API in under five minutes.

## Prerequisites

- A BookStore API key (see [Authentication](authentication.md))
- A tool for making HTTP requests: `curl`, Postman, or any HTTP client library

## Step 1 â€” Set Your API Key

Store your API key as an environment variable:

```bash
# Windows PowerShell
$env:BOOKSTORE_API_KEY = "your_api_key_here"

# macOS / Linux
export BOOKSTORE_API_KEY="your_api_key_here"
```

## Step 2 â€” List All Books

Make your first API call to retrieve a list of books:

```bash
curl https://api.bookstore.example.com/v1/books   -H "Authorization: Bearer $env:BOOKSTORE_API_KEY"
```

Response:

```json
{
  "success": true,
  "data": [
    {
      "id": "book-001",
      "title": "The Great Gatsby",
      "author": { "id": "auth-001", "name": "F. Scott Fitzgerald" },
      "isbn": "9780743273565",
      "price": 12.99,
      "category": "Fiction",
      "stock": 42
    }
  ],
  "pagination": {
    "total": 1250,
    "page": 1,
    "perPage": 20,
    "totalPages": 63
  }
}
```

## Step 3 â€” Get a Single Book

```bash
curl https://api.bookstore.example.com/v1/books/book-001   -H "Authorization: Bearer $env:BOOKSTORE_API_KEY"
```

## Step 4 â€” Search for Books

```bash
curl "https://api.bookstore.example.com/v1/books?search=gatsby&category=Fiction"   -H "Authorization: Bearer $env:BOOKSTORE_API_KEY"
```

## Step 5 â€” Create an Order

```bash
curl -X POST https://api.bookstore.example.com/v1/orders   -H "Authorization: Bearer $env:BOOKSTORE_API_KEY"   -H "Content-Type: application/json"   -d '{
    "customerId": "cust-001",
    "items": [
      { "bookId": "book-001", "quantity": 2 },
      { "bookId": "book-002", "quantity": 1 }
    ],
    "shippingAddress": {
      "street": "123 Main St",
      "city": "New York",
      "country": "US",
      "postalCode": "10001"
    }
  }'
```

## Step 6 â€” Check Order Status

```bash
curl https://api.bookstore.example.com/v1/orders/ord-001   -H "Authorization: Bearer $env:BOOKSTORE_API_KEY"
```

## What's Next?

- Browse the full [Books API](../endpoints/books/list-books.md)
- Learn about [Pagination](../guides/pagination.md)
- Set up [Webhooks](../guides/webhooks.md) for real-time order updates
- Download the [OpenAPI Specification](../openapi/spec.md)

Last reviewed: October 2025.

