# Prompt Caching

## ELI5 (Explain Like I'm 5)

Imagine you work at a library. Every time someone asks you a question, you have to read the entire rulebook (1000 pages) before answering. That's slow and expensive.

**Prompt caching** means you read the rulebook once, remember it, and the next time someone asks — you skip the reading and answer directly.

Claude does the same thing. If you send the same long instructions every request, caching lets Claude "remember" them so you don't pay to re-send them every time.

---

## Without vs. With Caching

**Without caching** (every request):
```
[5000 token system prompt] + [10 token question] = 5010 tokens charged
[5000 token system prompt] + [10 token question] = 5010 tokens charged  ← again!
[5000 token system prompt] + [10 token question] = 5010 tokens charged  ← again!
```

**With caching:**
```
[5000 token system prompt] + [10 token question] = 5010 tokens  ← first time, full price
[cache hit]                + [10 token question] = ~10 tokens   ← 99% cheaper!
[cache hit]                + [10 token question] = ~10 tokens   ← 99% cheaper!
```

---

## How to use it

Add `"cache_control": {"type": "ephemeral"}` to the part you want cached:

```python
response = client.messages.create(
    model="claude-sonnet-4-6",
    system=[
        {
            "type": "text",
            "text": "You are a helpful assistant. Here are our full company policies: [... very long text ...]",
            "cache_control": {"type": "ephemeral"}  # Cache this!
        }
    ],
    messages=[{"role": "user", "content": "What is our refund policy?"}]
)
```

The cache lasts **5 minutes** — refreshed each time it's used.

---

## What's worth caching?

| Good to cache | Not worth caching |
|--------------|-------------------|
| Long system prompts | Short prompts (< 1000 tokens) |
| Large documents you reference | One-off requests |
| Codebases loaded as context | Unique questions |
| Full books / PDFs | Dynamic content that changes |

---

## The savings

- Cached tokens cost ~**90% less** than uncached tokens
- Cache writes cost slightly more (one-time)
- Break-even: if you reuse the cached content even twice, you save money

---

## One sentence summary

> Prompt caching saves money and speeds things up by letting Claude reuse your long instructions instead of reading them from scratch every time.
