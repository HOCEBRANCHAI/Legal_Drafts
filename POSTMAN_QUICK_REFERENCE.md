# Postman Quick Reference

## Your API URL
**Base URL:** `https://legaldrafts.onrender.com`

## ⚠️ IMPORTANT: Use POST Method

The `/api/generate-legal-draft` endpoint **REQUIRES POST method**. Using GET will give you a 405 Method Not Allowed error.

## Quick Test Request

### 1. Health Check (GET)
```
GET https://legaldrafts.onrender.com/health
```

### 2. Generate NDA (POST - Required!)
```
POST https://legaldrafts.onrender.com/api/generate-legal-draft

Headers:
Content-Type: application/json

Body:
{
  "template_type": "nda",
  "company_name": "TechCorp India Pvt Ltd",
  "registration_number": "U72900KA2020PTC123456",
  "registered_address": "123 Business Park, Bangalore, Karnataka 560066",
  "directors": ["John Doe"],
  "country": "India",
  "corporate_context": "SaaS AI Platform - NDA with ABC Consulting Services"
}
```

## All Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/` | API information |
| GET | `/health` | Health check |
| **POST** | `/api/generate-legal-draft` | **Generate legal document (POST REQUIRED!)** |

⚠️ **Common Error:** If you get "405 Method Not Allowed", make sure you're using **POST** method, not GET!

## Required Fields

- `template_type` (nda, employment, service, terms, board, shareholder)
- `company_name`
- `registration_number`
- `registered_address`

## Optional Fields

- `directors` (string, list, or list of objects)
- `country` (will be inferred from address if not provided)
- `corporate_context` (add any additional details here)

## Expected Response

```json
{
  "success": true,
  "draft_content": "# NON-DISCLOSURE AGREEMENT\n\n...",
  "metadata": {
    "template_type": "NDA",
    "applied_law": "India",
    "applied_context": "...",
    "company": "...",
    "signer": "..."
  }
}
```

