# Fix: 405 Method Not Allowed Error

## The Problem

You're getting a **405 Method Not Allowed** error when trying to generate a document.

## The Solution

You're using **GET** instead of **POST**. The `/api/generate-legal-draft` endpoint **only accepts POST requests**.

## Step-by-Step Fix in Postman

### Step 1: Check the Method Dropdown

Look at the top left of Postman, next to the URL bar:

```
❌ WRONG:
[GET ▼] https://legaldrafts.onrender.com/api/generate-legal-draft

✅ CORRECT:
[POST ▼] https://legaldrafts.onrender.com/api/generate-legal-draft
```

### Step 2: Change to POST

1. Click the dropdown that says **"GET"**
2. Select **"POST"** from the list
3. The URL should still be: `https://legaldrafts.onrender.com/api/generate-legal-draft`

### Step 3: Add Headers

1. Click the **"Headers"** tab
2. Add:
   - **Key:** `Content-Type`
   - **Value:** `application/json`

### Step 4: Add Body

1. Click the **"Body"** tab
2. Select **"raw"**
3. Select **"JSON"** from the dropdown
4. Paste this JSON:

```json
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

### Step 5: Send

Click the **"Send"** button. It should work now! ✅

## Visual Checklist

Before clicking Send, verify:

- [ ] Method is **POST** (not GET)
- [ ] URL is `https://legaldrafts.onrender.com/api/generate-legal-draft`
- [ ] Headers tab has `Content-Type: application/json`
- [ ] Body tab is selected
- [ ] Body is set to **raw** and **JSON**
- [ ] JSON body contains all required fields

## Why POST is Required

The endpoint needs to:
1. Accept a JSON request body with your document parameters
2. Process the data and generate a document
3. Return the generated document

GET requests cannot have request bodies, so POST is required.

## Quick Test

Try this in Postman:

**Method:** POST  
**URL:** `https://legaldrafts.onrender.com/health`

This should return:
```json
{
  "status": "healthy",
  "service": "legal-document-generator"
}
```

If this works, your Postman setup is correct. Then try the generate endpoint with POST method.


