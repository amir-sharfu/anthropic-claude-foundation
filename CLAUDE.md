# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Purpose

This repo is a plain-English reference for foundational Anthropic Claude concepts — ELI5-style guides, runnable examples, and resources. Content is added incrementally by topic. All writing should be simple and accessible (no heavy jargon).

## Repository Structure

- `docs/eli5/` — ELI5 concept guides (Markdown, numbered 01–09+)
- `examples/` — runnable code demos, organized by topic (primarily Python using the `anthropic` SDK)
- `resources/` — reference material, links, cheat sheets

## ELI5 Guides (docs/eli5/)

| File | Topic |
|------|-------|
| 01-what-is-claude.md | Overview of Claude |
| 02-api-basics.md | Requests, responses, tokens, API keys |
| 03-prompt-engineering.md | Writing better prompts |
| 04-tool-use.md | Function/tool calling |
| 05-vision-multimodal.md | Images + text inputs |
| 06-extended-thinking.md | Step-by-step reasoning mode |
| 07-agents-automation.md | Autonomous agent loops |
| 08-prompt-caching.md | Caching long prompts for cost savings |
| 09-batch-processing.md | Async bulk requests at 50% cost |

## Writing Conventions

- ELI5 tone throughout — explain like the reader is smart but new to AI
- Each doc follows: analogy → how it works → code example → table summary → one-sentence summary
- API keys and tokens go in `.env` files (never committed — already in `.gitignore`)
- Python examples use the `anthropic` SDK (`pip install anthropic`)
- New topics: add a doc in `docs/eli5/` and example(s) in `examples/`
