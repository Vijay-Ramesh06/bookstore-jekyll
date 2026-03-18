---
layout: docs
version: v1.0
title: "Testing"
---

# Testing with OpenAPI Tools

The BookStore API's OpenAPI specification enables interactive testing using a variety of tools. This page covers how to set up and use the most popular options.

## Swagger UI

Swagger UI provides a browser-based interface for browsing and testing all API endpoints.

### Running Swagger UI with Docker

```bash
docker run -d -p 8080:8080   -e SWAGGER_JSON_URL=https://api.bookstore.example.com/v1/openapi.json   swaggerapi/swagger-ui
```

Open `http://localhost:8080` in your browser. You will see a full interactive API reference.

To test authenticated endpoints:

1. Click **Authorize** at the top right
2. Enter `Bearer YOUR_API_KEY` in the Value field
3. Click **Authorize** and close the dialog
4. All subsequent requests will include your API key

### Running Swagger UI without Docker

```bash
npm install -g http-server
curl -O https://api.bookstore.example.com/v1/openapi.json
# Create a simple HTML file embedding the Swagger UI CDN
http-server .
```

## Postman

### Import via URL

1. Open Postman and click **Import**
2. Select the **Link** tab
3. Paste `https://api.bookstore.example.com/v1/openapi.json`
4. Click **Continue** and then **Import**

### Set Up Environment Variables

1. Click **Environments** in the sidebar
2. Create a new environment called `BookStore Production`
3. Add a variable: `apiKey` = `your_api_key_here`
4. Add a variable: `baseUrl` = `https://api.bookstore.example.com/v1`
5. Select this environment before making requests

Now your imported collection will automatically use these variables.

### Running All Requests

Use Postman's **Collection Runner** to run all imported requests as a test suite:

1. Right-click the imported collection
2. Select **Run collection**
3. Configure the number of iterations and delay
4. Click **Run BookStore API**

## Insomnia

1. Open Insomnia and click **Create** Ã¢â€ â€™ **Import**
2. Select **From URL**
3. Enter `https://api.bookstore.example.com/v1/openapi.json`

Insomnia automatically creates a request collection with all endpoints.

## VS Code REST Client Extension

Create a `.http` file in your project:

```http
@baseUrl = https://api.bookstore.example.com/v1
@apiKey = your_api_key_here

### List all books
GET {{baseUrl}}/books?category=Fiction
Authorization: Bearer {{apiKey}}

### Get a specific book
GET {{baseUrl}}/books/book-001
Authorization: Bearer {{apiKey}}

### Create a book
POST {{baseUrl}}/books
Authorization: Bearer {{apiKey}}
Content-Type: application/json

{
  "title": "New Test Book",
  "authorId": "auth-001",
  "isbn": "9780000000099",
  "price": 15.99,
  "categoryId": "cat-001"
}
```

Click **Send Request** above each block to execute it. Results appear in a side panel.

## Validating Requests Against the Schema

Use the `ajv` library to validate request bodies before sending:

```javascript
const Ajv = require('ajv');
const spec = require('./openapi.json');

const ajv = new Ajv();
const validate = ajv.compile(spec.components.schemas.Book);

const newBook = { title: 'Test', isbn: 'bad' };
const valid = validate(newBook);
if (!valid) {
  console.error('Validation errors:', validate.errors);
}
```


