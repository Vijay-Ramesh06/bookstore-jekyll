---
layout: docs
version: v1.0
title: "Overview"
---

# OpenAPI Overview

The BookStore API is fully described using the OpenAPI 3.0 specification. This allows you to generate client libraries, import into API testing tools, and validate requests automatically.

## What is OpenAPI?

OpenAPI (formerly known as Swagger) is an open standard for describing REST APIs. An OpenAPI specification is a machine-readable document (JSON or YAML) that describes every endpoint, parameter, request body, and response of an API.

## BookStore API Specification

The BookStore API OpenAPI specification is available at:

```
https://api.bookstore.example.com/v1/openapi.json
```

YAML version:

```
https://api.bookstore.example.com/v1/openapi.yaml
```

## Using the Specification

### Import into Postman

1. Open Postman
2. Click **Import** Ã¢â€ â€™ **Link**
3. Paste `https://api.bookstore.example.com/v1/openapi.json`
4. Click **Continue** Ã¢â€ â€™ **Import**

All endpoints are now available as a Postman collection with pre-filled request structures.

### Import into Insomnia

1. Open Insomnia
2. Click **Create** Ã¢â€ â€™ **Import From URL**
3. Paste the OpenAPI specification URL

### Use with Swagger UI

Run a local Swagger UI instance:

```bash
docker run -p 8080:8080   -e SWAGGER_JSON_URL=https://api.bookstore.example.com/v1/openapi.json   swaggerapi/swagger-ui
```

Open `http://localhost:8080` to browse and test all endpoints interactively.

## Generating Client Libraries

Use the OpenAPI Generator to create client libraries in your preferred language:

```bash
# Install OpenAPI Generator
npm install -g @openapitools/openapi-generator-cli

# Generate a JavaScript client
openapi-generator-cli generate   -i https://api.bookstore.example.com/v1/openapi.json   -g javascript   -o ./bookstore-client-js

# Generate a Python client
openapi-generator-cli generate   -i https://api.bookstore.example.com/v1/openapi.json   -g python   -o ./bookstore-client-python
```

## Specification Structure

The BookStore API OpenAPI spec is organized into the following sections:

| Section | Description |
|---|---|
| `info` | API title, version, and contact information |
| `servers` | Base URLs for production and staging |
| `paths` | All endpoint definitions |
| `components/schemas` | Reusable data models |
| `components/securitySchemes` | Authentication definitions |
| `tags` | Endpoint groupings |


