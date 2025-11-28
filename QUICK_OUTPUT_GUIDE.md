# Quick Guide: Understanding Your Output

## ✅ Your Output is CORRECT!

The output you're seeing is **perfectly normal**. The `\n` and `**` symbols are just how JSON represents the text. The actual content is clean, properly formatted Markdown.

## Two Ways to Get Your Document

### Option 1: Get Plain Text (Easiest to Read) ✨ NEW!

Add `?format=text` to your URL to get clean markdown directly:

**In Postman:**
```
POST https://legaldrafts.onrender.com/api/generate-legal-draft?format=text
```

**What you'll get:**
- Clean markdown text (no JSON, no `\n` symbols)
- Properly formatted with real line breaks
- Ready to copy and use immediately

**Example:**
```
POST https://legaldrafts.onrender.com/api/generate-legal-draft?format=text

Body: (same JSON as before)
{
  "template_type": "employment",
  "company_name": "Strategic Consulting Ltd",
  ...
}
```

**Response:** Clean markdown text directly (no JSON wrapper)

---

### Option 2: Get JSON (Default - Includes Metadata)

**In Postman:**
```
POST https://legaldrafts.onrender.com/api/generate-legal-draft
```

**What you'll see:**
```json
{
  "draft_content": "**EMPLOYMENT AGREEMENT**\n\n---\n\n...",
  "metadata": { ... }
}
```

**How to extract clean markdown:**

**Method A: In Postman**
1. Click on the `draft_content` value
2. Copy it (Postman will handle the `\n` conversion)
3. Paste into a text editor - it will be clean!

**Method B: Using Python**
```python
import requests

response = requests.post("https://legaldrafts.onrender.com/api/generate-legal-draft", json={
    "template_type": "employment",
    "company_name": "Strategic Consulting Ltd",
    "registration_number": "12345678",
    "registered_address": "10 Downing Street, London, UK, SW1A 2AA",
    "directors": ["David Brown"],
    "country": "UK",
    "corporate_context": "Management Consulting - Hiring Sarah Williams as Senior Consultant for £75,000 per annum"
})

result = response.json()
draft = result["draft_content"]  # This is clean markdown!

# Save to file
with open("employment_agreement.md", "w", encoding="utf-8") as f:
    f.write(draft)

# Print it (will show with proper line breaks)
print(draft)
```

---

## Understanding the Symbols

| Symbol | What It Means | In JSON | When Extracted |
|--------|---------------|---------|----------------|
| `\n` | New line | Shows as `\n` | Becomes actual line break |
| `**text**` | Bold text | Shows as `**text**` | Markdown for bold (renders as **bold** in markdown viewers) |
| `---` | Horizontal rule | Shows as `---` | Creates a line separator |

## Quick Comparison

### JSON Response (Default)
```json
{
  "draft_content": "**EMPLOYMENT AGREEMENT**\n\n---\n\n**PARTIES:**\n\n..."
}
```
- ✅ Includes metadata
- ✅ Easy to parse programmatically
- ⚠️ Shows `\n` in JSON (but extracts cleanly)

### Plain Text Response (`?format=text`)
```
**EMPLOYMENT AGREEMENT**

---

**PARTIES:**

...
```
- ✅ Clean, readable immediately
- ✅ No JSON wrapper
- ✅ Perfect for quick viewing
- ❌ No metadata included

## Recommendation

- **For quick viewing/testing:** Use `?format=text`
- **For production/integration:** Use default JSON (includes metadata)
- **For saving files:** Extract `draft_content` from JSON or use `format=text`

## Example: Using format=text in Postman

1. **Method:** POST
2. **URL:** `https://legaldrafts.onrender.com/api/generate-legal-draft?format=text`
3. **Headers:** `Content-Type: application/json`
4. **Body:** (your JSON request)

**Result:** You'll see clean markdown directly in the response body! 🎉

