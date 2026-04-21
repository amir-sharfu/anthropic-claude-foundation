# Batch Processing

## ELI5 (Explain Like I'm 5)

Imagine you need 1000 letters written. You could:
- **Option A:** Write one letter, send it, wait for a reply, write the next one... (1000 round trips, slow)
- **Option B:** Write all 1000 letters, put them in a mailbag, send it all at once, come back tomorrow to pick up all the replies (1 trip, cheap)

**Batch processing** is Option B. Instead of asking Claude one question at a time, you send thousands of questions at once, Claude processes them in the background, and you pick up all the answers later.

---

## Normal vs. Batch

| | Normal API | Batch API |
|---|-----------|-----------|
| Speed | Instant reply | Results ready within 24h |
| Cost | Full price | **~50% cheaper** |
| Use when | You need answers NOW | You can wait |
| Volume | Any size | Up to 100,000 requests per batch |

---

## How it works

### Step 1: Submit a batch

```python
batch = client.messages.batches.create(
    requests=[
        {
            "custom_id": "email-001",
            "params": {
                "model": "claude-sonnet-4-6",
                "max_tokens": 100,
                "messages": [{"role": "user", "content": "Classify this email as spam or not: 'You won a prize!'"}]
            }
        },
        {
            "custom_id": "email-002",
            "params": {
                "model": "claude-sonnet-4-6",
                "max_tokens": 100,
                "messages": [{"role": "user", "content": "Classify this email as spam or not: 'Meeting at 3pm tomorrow'"}]
            }
        }
        # ... up to 100,000 more
    ]
)
print(batch.id)  # keep this to check results later
```

### Step 2: Check if it's done

```python
batch = client.messages.batches.retrieve(batch.id)
print(batch.processing_status)  # "in_progress" or "ended"
```

### Step 3: Get the results

```python
for result in client.messages.batches.results(batch.id):
    print(result.custom_id, result.result.message.content[0].text)
# email-001  This is spam.
# email-002  This is not spam.
```

---

## Best use cases

| Task | Volume |
|------|--------|
| Classify emails | 10,000 emails |
| Translate documents | 1,000 articles |
| Generate product descriptions | 500 items |
| Summarize support tickets | 5,000 tickets |
| Extract data from forms | 2,000 PDFs |

---

## Key rules

- Batches are processed **within 24 hours** (usually much faster)
- Max **100,000 requests** per batch
- Results stay available for **29 days**
- Each request in the batch is independent

---

## One sentence summary

> Batch processing lets you send thousands of questions to Claude at once, get them all processed in the background, and pick up the answers later — at half the price.
