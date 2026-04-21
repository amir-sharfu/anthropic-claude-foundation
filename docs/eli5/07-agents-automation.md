# Agents & Automation

## ELI5 (Explain Like I'm 5)

Normally, you give Claude one question and it gives one answer. An **agent** is different — you give Claude a **goal**, and it figures out all the steps needed to reach that goal by itself.

Think of it like the difference between:
- Asking someone "what's the weather?" (one question, one answer)
- Asking someone "plan my trip to Paris" (they research flights, hotels, weather, activities — all on their own)

---

## The Agent Loop

An agent works in a loop:

```
1. Look at the goal
2. Decide what to do next
3. Use a tool (search, run code, read a file, etc.)
4. See the result
5. Repeat until the goal is done
```

You set the goal. The agent figures out the steps.

---

## Simple Example

```python
# Goal: "Research the top 3 AI companies and write a summary"
# The agent might:
#   1. Call search_web("top AI companies 2025")
#   2. Read the results
#   3. Call search_web("Anthropic overview")
#   4. Call search_web("OpenAI overview")
#   5. Call search_web("Google DeepMind overview")
#   6. Write a summary combining all results

response = client.messages.create(
    model="claude-sonnet-4-6",
    tools=[search_web_tool],
    messages=[{
        "role": "user",
        "content": "Research the top 3 AI companies and write a 1-paragraph summary of each"
    }]
)
# Claude will automatically call tools as many times as needed
```

---

## Agents vs. Single Calls

| Single Call | Agent |
|-------------|-------|
| One question → one answer | One goal → many steps |
| You control each step | Claude controls the steps |
| Predictable | Flexible |
| Simple tasks | Complex, multi-step tasks |

---

## Building blocks of an agent

1. **A model** — Claude does the thinking
2. **Tools** — what Claude can do (search, write files, call APIs)
3. **Memory** — context from previous steps (the conversation history)
4. **A loop** — run until the goal is done

---

## When to use agents

- Research and summarization across many sources
- Automated coding tasks (write, test, fix, repeat)
- Data pipelines (fetch → transform → store)
- Customer support automation
- Anything with multiple dependent steps

---

## One sentence summary

> An agent is Claude working autonomously toward a goal — it plans, uses tools, checks results, and repeats until the job is done.
