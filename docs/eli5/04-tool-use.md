# Tool Use

## ELI5 (Explain Like I'm 5)

By default, Claude can only think and talk. It knows a lot from training, but it can't check live information, run code, or interact with the world.

**Tools** are like giving Claude a toolbox. You define the tools, Claude decides which one to pick and when to use it.

---

## The Analogy

Claude without tools = a very smart person locked in a room with no phone, no computer, no internet.

Claude with tools = that same person, but now they have a phone, a calculator, and can send emails.

---

## How Tool Use Works

```
1. You define tools (e.g. get_weather, search_web)
2. You ask Claude a question
3. Claude reads the question and decides: "I need to use get_weather here"
4. Claude calls the tool with the right inputs
5. Your code runs the tool and sends back the result
6. Claude uses the result to write its final answer
```

You run the tool — Claude just decides when and how to call it.

---

## Simple Example

```python
tools = [
    {
        "name": "get_weather",
        "description": "Get the current weather for a city",
        "input_schema": {
            "type": "object",
            "properties": {
                "city": {"type": "string", "description": "City name"}
            },
            "required": ["city"]
        }
    }
]

response = client.messages.create(
    model="claude-sonnet-4-6",
    tools=tools,
    messages=[{"role": "user", "content": "What's the weather in Paris?"}]
)
# Claude will call get_weather(city="Paris")
```

---

## Common Tools People Build

| Tool | What it does |
|------|-------------|
| `search_web(query)` | Search the internet |
| `get_weather(city)` | Get live weather |
| `run_sql(query)` | Query a database |
| `send_email(to, body)` | Send an email |
| `read_file(path)` | Read a file from disk |
| `run_python(code)` | Execute Python code |

---

## Key Point

You define the tools. You run the tools. Claude just decides **which** tool to call and **what** to pass in.

---

## One sentence summary

> Tools give Claude the ability to interact with the real world — you give it a toolbox, it figures out which tool to grab.
