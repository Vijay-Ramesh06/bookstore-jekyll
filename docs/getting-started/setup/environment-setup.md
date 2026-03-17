---
layout: docs
title: "Environment Setup"
---

# Environment Setup

Before making API requests, set up your development environment properly. This guide covers environment variables, testing tools, and recommended project structure.

## Setting Up Environment Variables

Never hardcode your API key in source code. Always use environment variables.

### Windows PowerShell

```powershell
$env:BOOKSTORE_API_KEY = "your_api_key_here"
$env:BOOKSTORE_BASE_URL = "https://api.bookstore.example.com/v1"
```

To persist across sessions, add it to your PowerShell profile:

```powershell
notepad $PROFILE
# Add the lines above and save
```

### macOS and Linux

```bash
export BOOKSTORE_API_KEY="your_api_key_here"
export BOOKSTORE_BASE_URL="https://api.bookstore.example.com/v1"
```

Add these lines to your `~/.bashrc` or `~/.zshrc` to persist across sessions.

## Using a .env File

For project-based environments, use a `.env` file:

```
BOOKSTORE_API_KEY=your_api_key_here
BOOKSTORE_BASE_URL=https://api.bookstore.example.com/v1
```

Load it using `dotenv` in JavaScript:

```bash
npm install dotenv
```

```javascript
require('dotenv').config();
const API_KEY = process.env.BOOKSTORE_API_KEY;
```

Or in Python:

```bash
pip install python-dotenv
```

```python
from dotenv import load_dotenv
load_dotenv()
API_KEY = os.getenv('BOOKSTORE_API_KEY')
```

**Important:** Add `.env` to your `.gitignore` to prevent accidental commits.

## Testing with cURL

cURL is the simplest way to test API endpoints without installing any library.

### Basic GET request

```powershell
curl "https://api.bookstore.example.com/v1/books" `
  -H "Authorization: Bearer $env:BOOKSTORE_API_KEY"
```

### POST request with body

```powershell
curl -X POST "https://api.bookstore.example.com/v1/orders" `
  -H "Authorization: Bearer $env:BOOKSTORE_API_KEY" `
  -H "Content-Type: application/json" `
  -d '{"customerId": "cust-001", "items": [{"bookId": "book-001", "quantity": 1}]}'
```

## Staging Environment

A staging environment is available for testing without affecting production data:

```
https://staging-api.bookstore.example.com/v1
```

Use the same API key format but generate a separate staging key from the developer portal. Staging data is reset every 24 hours.

## Recommended Tools

| Tool | Purpose | Download |
|---|---|---|
| Postman | GUI API testing | postman.com |
| Insomnia | Lightweight API client | insomnia.rest |
| cURL | Command-line testing | Built into most systems |
| VS Code REST Client | API testing inside VS Code | VS Code extension |

## Project Structure Recommendation

For applications integrating the BookStore API:

```
my-app/
â”œâ”€â”€ .env                    # API keys (never commit)
â”œâ”€â”€ .gitignore              # Include .env
â”œâ”€â”€ src/
â”‚   â”œâ”€â”€ api/
â”‚   â”‚   â”œâ”€â”€ client.js       # HTTP client setup
â”‚   â”‚   â”œâ”€â”€ books.js        # Books API calls
â”‚   â”‚   â”œâ”€â”€ orders.js       # Orders API calls
â”‚   â”‚   â””â”€â”€ customers.js    # Customers API calls
â”‚   â””â”€â”€ app.js
â””â”€â”€ package.json
```

Keeping API calls in a dedicated `api/` folder makes it easy to update base URLs or authentication without touching application logic.


