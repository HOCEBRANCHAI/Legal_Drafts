# Understanding the API Output

## The Output Format

When you receive a response from the API, the `draft_content` field contains **clean, properly formatted Markdown**. 

### What You See in JSON

In the JSON response, you might see things like:
```json
{
  "draft_content": "**EMPLOYMENT AGREEMENT**\n\n---\n\n**PARTIES:**\n\n..."
}
```

**Don't worry!** The `\n` (newlines) and `**` (bold markers) are just how JSON represents the text. The actual content is clean Markdown.

## How to Extract the Clean Markdown

### Method 1: Copy from JSON Response (Postman/Browser)

1. In Postman, click on the `draft_content` value
2. Copy the entire string (including the quotes)
3. Paste it into a text editor
4. The newlines (`\n`) will automatically convert to actual line breaks when you paste

### Method 2: Use Python/JavaScript

**Python:**
```python
import requests
import json

response = requests.post("https://legaldrafts.onrender.com/api/generate-legal-draft", json={
    "template_type": "nda",
    "company_name": "TechCorp India Pvt Ltd",
    "registration_number": "U72900KA2020PTC123456",
    "registered_address": "123 Business Park, Bangalore, Karnataka 560066",
    "directors": ["John Doe"],
    "country": "India",
    "corporate_context": "SaaS AI Platform"
})

result = response.json()
draft = result["draft_content"]  # This is already clean markdown!

# Save to file
with open("draft.md", "w", encoding="utf-8") as f:
    f.write(draft)

# Or print it (newlines will display correctly)
print(draft)
```

**JavaScript/Node.js:**
```javascript
const response = await fetch('https://legaldrafts.onrender.com/api/generate-legal-draft', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    template_type: "nda",
    company_name: "TechCorp India Pvt Ltd",
    registration_number: "U72900KA2020PTC123456",
    registered_address: "123 Business Park, Bangalore, Karnataka 560066",
    directors: ["John Doe"],
    country: "India",
    corporate_context: "SaaS AI Platform"
  })
});

const result = await response.json();
const draft = result.draft_content; // Clean markdown!

// Save to file
const fs = require('fs');
fs.writeFileSync('draft.md', draft);
```

### Method 3: Use Online JSON Parser

1. Copy the entire JSON response
2. Go to https://jsonformatter.org/json-parser
3. Paste and parse
4. Copy the `draft_content` value
5. The newlines will be properly formatted

## What the Clean Markdown Looks Like

When extracted properly, your document will look like this:

```markdown
**EMPLOYMENT AGREEMENT**

---

**PARTIES:**

This Employment Agreement ("Agreement") is made and entered into by and between Strategic Consulting Ltd...

**SECTION 1: APPOINTMENT & DUTIES**

1.1 **Title:** The Employee is hereby appointed as a Senior Consultant.
...
```

## Using the Markdown

### View as Formatted Document

1. **Save as `.md` file** and open in:
   - GitHub (renders markdown beautifully)
   - VS Code (with markdown preview)
   - Any markdown viewer

2. **Convert to PDF/DOCX:**
   - Use online converters like https://www.markdowntopdf.com/
   - Or use Pandoc: `pandoc draft.md -o draft.pdf`

### Edit the Document

The markdown is clean and editable:
- `**text**` = bold text
- `---` = horizontal rule
- `# Heading` = section headers
- Regular text = body content

You can:
1. Edit directly in any text editor
2. Add/remove sections
3. Modify clauses
4. Save and use as needed

## Important Notes

✅ **The output is already clean** - No need to manually remove `\n` or `**`  
✅ **Markdown format** - Standard markdown that works everywhere  
✅ **Ready to use** - Can be copied, edited, and converted to other formats  
✅ **Properly formatted** - Sections, headers, and formatting are correct  

## Example: Complete Workflow

```python
import requests

# 1. Generate document
response = requests.post("https://legaldrafts.onrender.com/api/generate-legal-draft", json={
    "template_type": "employment",
    "company_name": "My Company Ltd",
    "registration_number": "123456",
    "registered_address": "123 Main St, London, UK",
    "directors": ["John Doe"],
    "country": "UK",
    "corporate_context": "Hiring Sarah Williams as Senior Developer for £80,000"
})

# 2. Extract clean markdown
result = response.json()
draft = result["draft_content"]

# 3. Save to file
with open("employment_agreement.md", "w", encoding="utf-8") as f:
    f.write(draft)

# 4. Now you can:
# - Open in VS Code to preview
# - Edit the markdown
# - Convert to PDF
# - Share with legal team
```

## Troubleshooting

**Q: I see `\n` in my output, is that normal?**  
A: Yes! In JSON, newlines are represented as `\n`. When you extract the value (using code or copying), they become actual line breaks.

**Q: The markdown has `**` symbols, is that correct?**  
A: Yes! `**text**` is markdown syntax for bold text. When viewed in a markdown viewer, it will appear as bold.

**Q: How do I get plain text without markdown?**  
A: You can use a markdown-to-text converter, or simply remove the `**` symbols manually if you need plain text.

**Q: Can I get HTML or PDF directly?**  
A: Not from the API, but you can easily convert the markdown to HTML/PDF using tools like Pandoc or online converters.

