# Claude API Basics

## ELI5 (Explain Like I'm 5)

Imagine a restaurant. You are the customer, Claude is the chef, and the **API** is the waiter. You tell the waiter what you want, the waiter goes to the chef, the chef cooks it, and the waiter brings it back to you.

The **API** (Application Programming Interface) is just the official way your app talks to Claude. You send a message, you get a message back.

---

## The Flow

```
Your App  →  Anthropic API  →  Claude
Your App  ←  Anthropic API  ←  Claude
```

Your code sends a **request**. Claude sends back a **response**. That's the whole loop.

---

## What you send (Request)

```python
import anthropic

client = anthropic.Anthropic()  # uses ANTHROPIC_API_KEY from environment

message = client.messages.create(
    model="claude-sonnet-4-6",
    max_tokens=1024,
    messages=[
        {"role": "user", "content": "Hello Claude!"}
    ]
)
```

Key pieces:
| Field | What it means |
|-------|--------------|
| `model` | Which version of Claude to use |
| `max_tokens` | Max length of the reply (like a word limit) |
| `messages` | The conversation — what you said |

---

## What you get back (Response)

```python
print(message.content[0].text)
# "Hi there! How can I help you today?"

print(message.usage)
# input_tokens=10, output_tokens=14
```

Claude sends back text + info about how many **tokens** were used (tokens = roughly words, used for billing).

---

## The API Key

To use the API you need an **API key** — like a password that proves you have an account.

```bash
ANTHROPIC_API_KEY=sk-ant-...
```

**Rules:**
- Store it in a `.env` file, never in your code
- Never commit it to git
- Never share it with anyone

---

## Tokens — the currency of the API

Claude doesn't count words, it counts **tokens**. Roughly:
- 1 token ≈ 1 word (sometimes shorter words, sometimes longer)
- 100 tokens ≈ 75 words
- You pay based on tokens in + tokens out

---

## One sentence summary

> The Claude API is the door between your app and Claude — you knock with a request, Claude answers with a response.
