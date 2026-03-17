---
layout: docs
title: "Pagination"
---

# Pagination

All BookStore API list endpoints return paginated results. This guide explains how pagination works and how to iterate through large result sets.

## Pagination Parameters

| Parameter | Type | Default | Max | Description |
|---|---|---|---|---|
| `page` | integer | 1 | â€” | Page number to retrieve |
| `perPage` | integer | 20 | 100 | Number of results per page |

## Pagination Response Object

Every list endpoint includes a `pagination` object in the response:

```json
{
  "pagination": {
    "total": 1250,
    "page": 2,
    "perPage": 20,
    "totalPages": 63
  }
}
```

| Field | Description |
|---|---|
| `total` | Total number of matching records |
| `page` | Current page number |
| `perPage` | Number of records per page |
| `totalPages` | Total number of pages |

## Fetching All Pages in JavaScript

```javascript
async function getAllBooks() {
  const books = [];
  let page = 1;
  let totalPages = 1;

  while (page <= totalPages) {
    const response = await fetch(
      `https://api.bookstore.example.com/v1/books?page=${page}&perPage=100`,
      { headers: { 'Authorization': `Bearer ${API_KEY}` } }
    );
    const json = await response.json();
    books.push(...json.data);
    totalPages = json.pagination.totalPages;
    page++;
  }

  return books;
}
```

## Fetching All Pages in Python

```python
def get_all_books():
    books = []
    page = 1
    total_pages = 1

    while page <= total_pages:
        response = requests.get(
            f'{BASE_URL}/books',
            params={'page': page, 'perPage': 100},
            headers=headers
        )
        data = response.json()
        books.extend(data['data'])
        total_pages = data['pagination']['totalPages']
        page += 1

    return books
```

## Best Practices

- Use `perPage=100` to minimize the number of API calls when fetching large datasets
- Cache the `total` and `totalPages` values from the first response to avoid unnecessary requests
- For very large datasets, consider using date-range filters to split the data into smaller chunks
- Respect rate limits by adding a small delay between requests when iterating many pages

Last reviewed: October 2025.


