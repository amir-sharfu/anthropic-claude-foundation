# Extended Thinking

## ELI5 (Explain Like I'm 5)

Imagine you ask a friend a hard math question. They could answer immediately (maybe wrong), or they could say "hold on, let me think through this carefully" and work it out step by step on paper before giving you the answer.

**Extended thinking** is Claude choosing to "work it out on paper first." It thinks through a problem step by step before giving its final answer — and gets a lot more accurate.

---

## Normal vs. Extended Thinking

| | Normal | Extended Thinking |
|---|--------|-------------------|
| Speed | Fast | Slower |
| Accuracy on hard problems | Good | Much better |
| Shows reasoning | No | Yes (scratchpad) |
| Best for | Simple questions | Complex reasoning |

---

## How to enable it

```python
response = client.messages.create(
    model="claude-sonnet-4-6",
    max_tokens=16000,
    thinking={
        "type": "enabled",
        "budget_tokens": 10000  # how much thinking Claude can do
    },
    messages=[{"role": "user", "content": "Solve this step by step: ..."}]
)
```

`budget_tokens` controls how long Claude can "think" before answering. More budget = more thorough reasoning.

---

## Reading Claude's thoughts

The response contains two parts — the thinking and the answer:

```python
for block in response.content:
    if block.type == "thinking":
        print("Claude's scratchpad:")
        print(block.thinking)  # Claude's internal reasoning
    elif block.type == "text":
        print("Final answer:")
        print(block.text)
```

---

## When to use it

| Good for | Not needed for |
|----------|---------------|
| Complex math | "What's 5+5?" |
| Logic puzzles | "Translate this to French" |
| Multi-step coding problems | "Summarize this text" |
| Strategic decisions | Simple factual questions |

---

## One sentence summary

> Extended thinking tells Claude to "think before it speaks" — it works through hard problems step by step and gives you a better, more reliable answer.
