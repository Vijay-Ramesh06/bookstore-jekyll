---
layout: docs
version: v1.0
title: "Testing"
---

# Testing Your Integration

This guide covers how to write tests for your BookStore API integration, including mocking, fixtures, and integration test patterns.

## Test Environments

Use the staging environment for all automated tests:

```
https://staging-api.bookstore.example.com/v1
```

Never run automated tests against the production API.

## Unit Testing with Mocks

Mock the API in unit tests so they run without network access.

### JavaScript (Jest)

```javascript
jest.mock('./api/books', () => ({
  listBooks: jest.fn().mockResolvedValue({
    success: true,
    data: [
      { id: 'book-001', title: 'The Great Gatsby', price: 12.99, stock: 42 }
    ],
    pagination: { total: 1, page: 1, perPage: 20, totalPages: 1 }
  }),
  getBook: jest.fn().mockResolvedValue({
    success: true,
    data: { id: 'book-001', title: 'The Great Gatsby', price: 12.99 }
  })
}));

test('displays book title', async () => {
  const books = await listBooks();
  expect(books.data[0].title).toBe('The Great Gatsby');
});
```

### Python (unittest.mock)

```python
from unittest.mock import patch, MagicMock

@patch('myapp.api.requests.get')
def test_list_books(mock_get):
    mock_get.return_value = MagicMock(
        ok=True,
        json=lambda: {
            'success': True,
            'data': [{'id': 'book-001', 'title': 'The Great Gatsby'}],
            'pagination': {'total': 1, 'page': 1, 'perPage': 20, 'totalPages': 1}
        }
    )
    result = list_books()
    assert result[0]['title'] == 'The Great Gatsby'
```

## Integration Tests

Integration tests call the real staging API.

```javascript
const API_KEY = process.env.BOOKSTORE_TEST_API_KEY;
const BASE_URL = 'https://staging-api.bookstore.example.com/v1';

describe('Books API', () => {
  test('GET /books returns a list', async () => {
    const res = await fetch(`${BASE_URL}/books`, {
      headers: { 'Authorization': `Bearer ${API_KEY}` }
    });
    const json = await res.json();
    expect(res.status).toBe(200);
    expect(json.success).toBe(true);
    expect(Array.isArray(json.data)).toBe(true);
    expect(json.pagination).toHaveProperty('total');
  });

  test('GET /books/:id returns 404 for invalid ID', async () => {
    const res = await fetch(`${BASE_URL}/books/invalid-id-9999`, {
      headers: { 'Authorization': `Bearer ${API_KEY}` }
    });
    expect(res.status).toBe(404);
  });
});
```

## Test Data Management

Create test data at the start of each test run and clean it up afterwards:

```javascript
let testBookId;

beforeAll(async () => {
  const res = await createBook({
    title: 'Test Book ' + Date.now(),
    authorId: 'auth-001',
    isbn: '9780000000001',
    price: 9.99,
    categoryId: 'cat-001'
  });
  testBookId = res.data.id;
});

afterAll(async () => {
  await deleteBook(testBookId);
});
```

## Testing Error Cases

Always write tests that verify error handling:

```javascript
test('returns 401 for missing API key', async () => {
  const res = await fetch(`${BASE_URL}/books`);
  const json = await res.json();
  expect(res.status).toBe(401);
  expect(json.error.code).toBe('INVALID_API_KEY');
});

test('returns 422 when creating book with invalid ISBN', async () => {
  const res = await createBook({ title: 'Test', isbn: 'bad-isbn' });
  expect(res.status).toBe(422);
  expect(json.error.fields).toContainEqual(
    expect.objectContaining({ field: 'isbn' })
  );
});
```


