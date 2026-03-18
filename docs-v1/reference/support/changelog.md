---
layout: docs
version: v1.0
title: "Changelog"
---

# API Changelog

This page documents all changes to the BookStore API, including new features, improvements, and breaking changes.

## v1.2.0 Ã¢â‚¬â€ 2025-09-01

### New Features

- **Review Filtering**: The `GET /v1/books/{bookId}/reviews` endpoint now supports filtering by `rating` and `verified` query parameters.
- **Inventory Alerts Webhook**: New webhook event `inventory.low` fires when a book's stock falls below its `reorderLevel`.
- **Bulk Book Update**: New endpoint `PATCH /v1/books/bulk` allows updating up to 50 books in a single request.
- **Author Books Endpoint**: New endpoint `GET /v1/authors/{authorId}/books` returns all books by a specific author with pagination.

### Improvements

- Improved search relevance for the `search` query parameter on `/v1/books`
- Order response now includes `estimatedDelivery` date
- Customer list endpoint now returns `totalSpent` and `lastOrderDate`
- API response times improved by approximately 15% for list endpoints

### Bug Fixes

- Fixed: Category `bookCount` not updating correctly after book deletion
- Fixed: Reviews from deleted customers causing 500 errors on book detail endpoint
- Fixed: Pagination `totalPages` rounding error for datasets with exact multiples of `perPage`

## v1.1.0 Ã¢â‚¬â€ 2025-04-15

### New Features

- **Webhook Support**: Full webhook system with event subscriptions and signature verification
- **Archive Endpoint**: Books can now be archived instead of deleted using `POST /v1/books/{bookId}/archive`
- **Review Summary**: Book detail response now includes rating distribution breakdown
- **Order Tracking**: Orders now include `trackingNumber` field once shipped

### Breaking Changes

None in this release.

### Improvements

- Added `tags` field to book create and update endpoints
- Rate limit headers now included in all responses, not just 429 responses
- Improved error messages for validation failures Ã¢â‚¬â€ now includes field-level details

## v1.0.0 Ã¢â‚¬â€ 2025-01-01

Initial public release of the BookStore API.

### Included

- Books CRUD endpoints
- Authors CRUD endpoints
- Orders endpoints (create, read, update, cancel)
- Customer management endpoints
- Category management endpoints
- Reviews endpoints
- Inventory management endpoints
- API key authentication
- Pagination, filtering, and sorting on all list endpoints
- OpenAPI 3.0 specification

Last reviewed: October 2025.

