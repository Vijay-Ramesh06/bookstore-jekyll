---
layout: docs
version: v1.0
title: "Filtering"
---

# Filtering

Most BookStore API list endpoints support query parameter filtering to retrieve exactly the data you need.

## Common Filter Parameters

### Text Search

Use the `search` parameter for full-text search across key fields:

```
GET /v1/books?search=fitzgerald
```

For books, this searches title, author name, description, and ISBN.

### Date Range Filters

Use ISO 8601 date format for date filters:

```
GET /v1/orders?fromDate=2025-01-01&toDate=2025-03-31
```

### Boolean Filters

```
GET /v1/books?inStock=true
```

### Enum Filters

```
GET /v1/orders?status=pending
GET /v1/orders?status=confirmed
```

## Combining Filters

All filters use AND logic Ã¢â‚¬â€ all conditions must match:

```
GET /v1/books?category=Fiction&inStock=true&minPrice=10&maxPrice=20
```

This returns Fiction books that are in stock and priced between $10 and $20.

## Filtering Books

| Filter | Description | Example |
|---|---|---|
| `search` | Search title, author, ISBN | `search=orwell` |
| `category` | Category ID or slug | `category=fiction` |
| `authorId` | Filter by author | `authorId=auth-001` |
| `minPrice` | Minimum price | `minPrice=5` |
| `maxPrice` | Maximum price | `maxPrice=25` |
| `inStock` | Only show in-stock books | `inStock=true` |
| `publishedYear` | Filter by year | `publishedYear=1984` |

## Filtering Orders

| Filter | Description | Example |
|---|---|---|
| `customerId` | Orders by customer | `customerId=cust-001` |
| `status` | Order status | `status=shipped` |
| `fromDate` | Orders after date | `fromDate=2025-01-01` |
| `toDate` | Orders before date | `toDate=2025-12-31` |
| `minAmount` | Minimum order total | `minAmount=50` |

## Filtering Reviews

| Filter | Description | Example |
|---|---|---|
| `rating` | Exact star rating | `rating=5` |
| `verified` | Only verified purchases | `verified=true` |


