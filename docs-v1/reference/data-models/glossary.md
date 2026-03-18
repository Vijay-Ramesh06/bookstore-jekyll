---
layout: docs
version: v1.0
title: "Glossary"
---

# Glossary

This page defines key terms used throughout the BookStore API documentation.

## A

**API Key**
A secret token used to authenticate requests to the BookStore API. API keys are generated in the developer portal and included in the `Authorization` header of every request.

**Author**
A person who wrote one or more books in the BookStore catalog. Authors are stored as separate records and linked to books via the `authorId` field.

## B

**Base URL**
The root URL for all API requests: `https://api.bookstore.example.com/v1`. All endpoint paths are appended to this base URL.

**Bearer Token**
The authentication scheme used by the BookStore API. The API key is passed as a Bearer token in the `Authorization` header: `Authorization: Bearer YOUR_API_KEY`.

**Book**
The primary resource in the BookStore API. Represents a physical or digital title available for sale, with fields for title, author, ISBN, price, category, and stock level.

## C

**Category**
A classification for books by genre or subject, such as Fiction, Non-Fiction, or Science Fiction. Books belong to exactly one category.

**CRUD**
Create, Read, Update, Delete Ã¢â‚¬â€ the four basic operations supported by the API for each resource type.

**Cursor**
A pointer used in some pagination implementations to mark the current position in a result set. The BookStore API uses page-based pagination rather than cursor-based.

**Customer**
A registered user of the bookstore who can place orders and submit reviews.

## E

**Endpoint**
A specific URL path in the API that handles a particular action or resource. For example, `GET /v1/books` is an endpoint for listing books.

**Event**
An action in the BookStore system that can trigger a webhook notification, such as `order.created` or `inventory.low`.

## I

**Idempotency Key**
A unique identifier attached to a request to ensure it is processed only once, even if retried. Prevents duplicate orders when a request times out and is retried.

**ISBN**
International Standard Book Number. A 13-digit identifier unique to each book edition. Used as a unique identifier for books in the BookStore system.

**Inventory**
The stock management record for a book, including current stock level, reserved units, reorder levels, and warehouse location.

## J

**JSON**
JavaScript Object Notation. The data format used for all BookStore API request bodies and responses.

## O

**OpenAPI**
An open standard for describing REST APIs. The BookStore API provides an OpenAPI 3.0 specification that can be imported into tools like Postman or used to generate client libraries.

**Order**
A purchase request from a customer containing one or more books, a shipping address, and payment information. Orders progress through statuses: pending, confirmed, shipped, delivered.

## P

**Pagination**
The practice of splitting large result sets into pages. The BookStore API uses page-based pagination with `page` and `perPage` query parameters.

**Payload**
The data body of an HTTP request or response, formatted as JSON.

**Permissions**
The level of access granted by an API key. BookStore API keys can be read-only, read-write, or admin.

## R

**Rate Limiting**
A restriction on the number of API requests allowed within a time window. Exceeding the limit returns a `429 Too Many Requests` error.

**REST**
Representational State Transfer. The architectural style followed by the BookStore API, using standard HTTP methods and consistent resource-based URLs.

**Review**
A customer rating and comment for a book, with a 1Ã¢â‚¬â€œ5 star rating and optional title and body text.

## S

**Schema**
The defined structure of a data object in the API. For example, the Book schema defines all fields returned when retrieving a book.

**Slug**
A URL-friendly version of a name, using lowercase letters and hyphens instead of spaces. For example, the slug for the category "Science Fiction" is `science-fiction`.

**Stock**
The number of physical units of a book currently held in the warehouse and available for sale.

## W

**Webhook**
A mechanism for the BookStore API to send HTTP notifications to your server when specific events occur, such as when an order is placed or a shipment is dispatched.


