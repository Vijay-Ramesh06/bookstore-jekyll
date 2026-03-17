---
layout: docs
title: "Sorting"
---

# Sorting

BookStore API list endpoints support sorting results by various fields using the `sort` and `order` query parameters.

## Sort Parameters

| Parameter | Description | Values |
|---|---|---|
| `sort` | Field to sort by | Varies by endpoint |
| `order` | Sort direction | `asc` or `desc` |

## Default Sort Behavior

If `sort` is not specified, results are returned in the default order for each resource:

| Resource | Default Sort | Default Order |
|---|---|---|
| Books | `createdAt` | `desc` (newest first) |
| Authors | `name` | `asc` (alphabetical) |
| Orders | `createdAt` | `desc` (newest first) |
| Customers | `createdAt` | `desc` |
| Reviews | `createdAt` | `desc` |

## Sortable Fields by Endpoint

### Books

| Field | Description |
|---|---|
| `title` | Alphabetical by title |
| `price` | By retail price |
| `publishedYear` | By year of publication |
| `averageRating` | By customer rating |
| `stock` | By stock level |
| `createdAt` | By date added to catalog |

```
GET /v1/books?sort=price&order=asc
```

### Orders

| Field | Description |
|---|---|
| `createdAt` | By order date |
| `totalAmount` | By order value |
| `status` | By order status |

```
GET /v1/orders?sort=totalAmount&order=desc
```

### Authors

| Field | Description |
|---|---|
| `name` | Alphabetical |
| `bookCount` | By number of books |
| `createdAt` | By date added |

## Sorting with Filtering

Sort and filter parameters work together:

```
GET /v1/books?category=Fiction&inStock=true&sort=price&order=asc&page=1&perPage=20
```

This returns in-stock Fiction books sorted from cheapest to most expensive.


