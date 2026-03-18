---
layout: docs
version: v1.0
title: "Schemas"
---

# Data Schemas

This page documents all data models used in the BookStore API.

## Book

```json
{
  "id": "book-001",
  "title": "The Great Gatsby",
  "author": {
    "id": "auth-001",
    "name": "F. Scott Fitzgerald"
  },
  "isbn": "9780743273565",
  "price": 12.99,
  "category": {
    "id": "cat-001",
    "name": "Fiction"
  },
  "description": "A novel set in the Jazz Age.",
  "publishedYear": 1925,
  "publisher": "Scribner",
  "language": "English",
  "pages": 180,
  "stock": 42,
  "averageRating": 4.2,
  "reviewCount": 128,
  "tags": ["classic", "american-literature"],
  "createdAt": "2024-01-01T00:00:00Z",
  "updatedAt": "2025-01-01T00:00:00Z"
}
```

## Author

```json
{
  "id": "auth-001",
  "name": "F. Scott Fitzgerald",
  "bio": "American novelist known for The Great Gatsby.",
  "nationality": "American",
  "birthYear": 1896,
  "deathYear": 1940,
  "website": "https://example.com",
  "bookCount": 4,
  "createdAt": "2024-01-01T00:00:00Z"
}
```

## Order

```json
{
  "id": "ord-001",
  "customer": { "id": "cust-001", "name": "Alice Smith" },
  "status": "confirmed",
  "items": [
    {
      "book": { "id": "book-001", "title": "The Great Gatsby" },
      "quantity": 2,
      "unitPrice": 12.99,
      "subtotal": 25.98
    }
  ],
  "subtotal": 25.98,
  "shippingCost": 4.99,
  "totalAmount": 30.97,
  "shippingAddress": {
    "street": "123 Main St",
    "city": "New York",
    "country": "US",
    "postalCode": "10001"
  },
  "trackingNumber": "TRK-ABC123",
  "createdAt": "2025-10-01T00:00:00Z"
}
```

## Customer

```json
{
  "id": "cust-001",
  "name": "Alice Smith",
  "email": "alice@example.com",
  "phone": "+1-555-0100",
  "orderCount": 12,
  "totalSpent": 189.45,
  "createdAt": "2024-03-15T00:00:00Z"
}
```

## Review

```json
{
  "id": "rev-001",
  "bookId": "book-001",
  "customer": { "id": "cust-001", "name": "Alice S." },
  "rating": 5,
  "title": "A timeless classic",
  "body": "One of the greatest novels ever written.",
  "verified": true,
  "createdAt": "2025-09-01T00:00:00Z"
}
```

## Inventory

```json
{
  "bookId": "book-001",
  "stock": 42,
  "reserved": 5,
  "available": 37,
  "reorderLevel": 10,
  "reorderQuantity": 50,
  "warehouseLocation": "Section A, Shelf 3",
  "lastRestocked": "2025-09-15T00:00:00Z"
}
```

## Address

```json
{
  "street": "123 Main St",
  "city": "New York",
  "state": "NY",
  "country": "US",
  "postalCode": "10001"
}
```


