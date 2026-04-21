# Vision & Multimodal

## ELI5 (Explain Like I'm 5)

Claude can do more than just read words — it can **look at images** too. Send Claude a photo along with your question, and it can see and describe what's in it.

This is called **multimodal** — "multi" means many, "modal" means type of input. So: text + images, not just text alone.

---

## What you can send

- Photos and screenshots
- Charts and graphs
- Diagrams and wireframes
- PDFs and scanned documents
- UI mockups

---

## How it works in code

```python
import anthropic, base64

with open("chart.png", "rb") as f:
    image_data = base64.standard_b64encode(f.read()).decode("utf-8")

message = client.messages.create(
    model="claude-sonnet-4-6",
    messages=[
        {
            "role": "user",
            "content": [
                {
                    "type": "image",
                    "source": {
                        "type": "base64",
                        "media_type": "image/png",
                        "data": image_data,
                    }
                },
                {
                    "type": "text",
                    "text": "What trend do you see in this chart?"
                }
            ]
        }
    ]
)
```

You can also send an image by URL:

```python
{
    "type": "image",
    "source": {
        "type": "url",
        "url": "https://example.com/chart.png"
    }
}
```

---

## Real-World Uses

| Use case | Example prompt |
|----------|---------------|
| Debug errors | "Here's a screenshot of the error — what's wrong?" |
| Read receipts | "Read this receipt and total up all the items" |
| Analyze data | "Look at this bar chart — which month had the highest sales?" |
| Build UIs | "Here's my wireframe — write the HTML and CSS for it" |
| Extract text | "Read the text in this handwritten note" |
| Understand diagrams | "Explain what this architecture diagram is showing" |

---

## Supported formats

- JPEG, PNG, GIF, WebP
- PDF (treated as a series of images)

---

## One sentence summary

> Claude can look at images and talk about them — just send a photo alongside your question and it will describe, analyze, or act on what it sees.
