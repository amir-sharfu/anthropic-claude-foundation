# Prompt Engineering

## ELI5 (Explain Like I'm 5)

A **prompt** is what you type to Claude. **Prompt engineering** is just learning how to ask better questions to get better answers.

Think of it like ordering at a restaurant. "Give me food" gets you something random. "I'd like a medium-rare cheeseburger with no onions" gets you exactly what you want.

---

## Vague vs. Clear

| Vague | Clear |
|-------|-------|
| "Write about dogs" | "Write a fun 3-sentence story about a golden retriever learning to swim" |
| "Fix my code" | "Fix the bug on line 12 — it should return a list, not a string" |
| "Summarize this" | "Summarize this in 5 bullet points for a non-technical audience" |

---

## 6 Tips for Better Prompts

### 1. Be Specific
Say exactly what you want — what topic, what length, what format.

```
Bad:  "Explain Python"
Good: "Explain what a Python list is, in 3 simple sentences, for a beginner"
```

### 2. Give Context
Tell Claude why you need it — it helps Claude give the right tone and depth.

```
"I'm presenting to my CEO tomorrow. Write a 1-paragraph summary of our Q3 results."
```

### 3. Give an Example
Show Claude the format you want.

```
"Format your response like this:
Title: ...
Summary: ...
Action items: ..."
```

### 4. Set a Role
Tell Claude who to be.

```
"You are an expert Python teacher. Explain decorators to a beginner."
```

### 5. Set Constraints
Tell Claude what limits to follow.

```
"Answer in under 100 words."
"Use only simple words, no jargon."
"Give exactly 5 suggestions."
```

### 6. Iterate
Your first prompt doesn't have to be perfect. Ask, see the output, then refine.

```
First: "Write a cover letter for a software engineer job"
Then:  "Make it shorter and more casual"
Then:  "Add a mention of my 5 years of Python experience"
```

---

## The System Prompt

You can also give Claude standing instructions at the start (the **system prompt**) — like briefing an assistant before they start work.

```python
messages.create(
    system="You are a friendly customer support agent. Always be polite and concise.",
    messages=[{"role": "user", "content": "My order is late"}]
)
```

---

## One sentence summary

> Prompt engineering is just learning to communicate clearly with Claude — the more specific and clear you are, the better the answer.
