---
layout: docs
version: v1.0
title: "Spec"
---

# OpenAPI Specification

Below is the core structure of the BookStore API OpenAPI 3.0 specification.

## Specification Header

```yaml
openapi: 3.0.3
info:
  title: BookStore API
  description: |
    A RESTful API for managing an online bookstore.
    Includes endpoints for books, authors, orders, customers,
    categories, reviews, and inventory.
  version: 1.0.0
  contact:
    name: BookStore API Support
    email: api-support@bookstore.example.com
    url: https://developers.bookstore.example.com

servers:
  - url: https://api.bookstore.example.com/v1
    description: Production
  - url: https://staging-api.bookstore.example.com/v1
    description: Staging

security:
  - BearerAuth: []
```

## Security Scheme

```yaml
components:
  securitySchemes:
    BearerAuth:
      type: http
      scheme: bearer
      bearerFormat: API Key
      description: |
        Include your API key in the Authorization header.
        Example: Authorization: Bearer YOUR_API_KEY
```

## Book Schema

```yaml
components:
  schemas:
    Book:
      type: object
      required: [title, authorId, isbn, price, categoryId]
      properties:
        id:
          type: string
          example: book-001
          readOnly: true
        title:
          type: string
          maxLength: 255
          example: The Great Gatsby
        authorId:
          type: string
          example: auth-001
        isbn:
          type: string
          pattern: '^[0-9]{13}$'
          example: "9780743273565"
        price:
          type: number
          format: float
          minimum: 0
          example: 12.99
        categoryId:
          type: string
          example: cat-001
        description:
          type: string
          example: A novel set in the Jazz Age.
        publishedYear:
          type: integer
          example: 1925
        stock:
          type: integer
          minimum: 0
          example: 42
          readOnly: true
        createdAt:
          type: string
          format: date-time
          readOnly: true
```

## Order Schema

```yaml
    Order:
      type: object
      required: [customerId, items, shippingAddress]
      properties:
        id:
          type: string
          readOnly: true
        customerId:
          type: string
        items:
          type: array
          items:
            $ref: '#/components/schemas/OrderItem'
        status:
          type: string
          enum: [pending, confirmed, shipped, delivered, cancelled]
          readOnly: true
        totalAmount:
          type: number
          readOnly: true
        shippingAddress:
          $ref: '#/components/schemas/Address'
        createdAt:
          type: string
          format: date-time
          readOnly: true

    OrderItem:
      type: object
      required: [bookId, quantity]
      properties:
        bookId:
          type: string
        quantity:
          type: integer
          minimum: 1
        unitPrice:
          type: number
          readOnly: true
```

## Tags

```yaml
tags:
  - name: Books
    description: Manage book listings
  - name: Authors
    description: Manage author profiles
  - name: Orders
    description: Place and track orders
  - name: Customers
    description: Manage customer accounts
  - name: Categories
    description: Book categories and genres
  - name: Reviews
    description: Customer book reviews
  - name: Inventory
    description: Stock management
```


