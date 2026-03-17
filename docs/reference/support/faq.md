---
layout: docs
title: "Faq"
---

# Frequently Asked Questions

## General

### Is the BookStore API free to use?

The API has a free tier allowing up to 60 requests per minute and 1,000 requests per day. Paid plans are available for higher volume. See the [Rate Limiting guide](../getting-started/rate-limiting.md) for tier details.

### Can I use the API for commercial projects?

Yes. The BookStore API is available for commercial use on all paid plans. Review the Terms of Service at `https://developers.bookstore.example.com/terms`.

### Is there an API sandbox for testing?

Yes. Use the staging environment at `https://staging-api.bookstore.example.com/v1`. Data in the staging environment is reset every 24 hours.

## Authentication

### What happens if I lose my API key?

You cannot recover a lost API key since it is shown only once at generation. Revoke the lost key from the developer portal and generate a new one.

### Can I have multiple API keys?

Yes. You can generate up to 10 API keys per account. Using separate keys for different applications or environments is recommended.

### Do API keys expire automatically?

Only if you set an expiry when creating the key. Keys without an expiry remain valid until manually revoked.

## Books and Catalog

### Can I add books without an existing author record?

No. Every book must reference an existing author via `authorId`. Create the author record first, then create the book.

### What ISBN formats are accepted?

Only ISBN-13 (13 digits, no hyphens) is accepted. ISBN-10 is not supported. If you have an ISBN-10, convert it to ISBN-13 before submitting.

### Can a book belong to multiple categories?

No. Each book belongs to exactly one category. Use tags for additional classification.

## Orders

### Can I modify an order after placing it?

You can update the shipping address and notes on orders with `pending` status. Once confirmed, only the tracking number can be added and the status can be changed by admins.

### What happens to stock when an order is placed?

Stock is reserved immediately when an order is created, reducing the `available` quantity. The `stock` quantity only changes when inventory is explicitly updated.

### How long are orders retained?

Order records are retained for 7 years for compliance purposes and cannot be deleted.

## Webhooks

### What happens if my webhook endpoint is down?

Taskify retries failed deliveries up to 5 times with exponential backoff. If all retries fail, the event is logged in the delivery history but not retried further.

### Can I receive all events on a single webhook?

Yes. When registering a webhook, subscribe to all event types you need. There is no limit on the number of event types per webhook endpoint.

## Data and Privacy

### Can I export all my data?

Yes. Contact `api-support@bookstore.example.com` to request a full data export in JSON format.

### How do I delete customer data for GDPR compliance?

Use `DELETE /v1/customers/{customerId}`. This anonymizes the customer record while preserving order history with anonymized customer references, as required for financial record-keeping.


