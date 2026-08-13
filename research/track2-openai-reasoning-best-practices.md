---
url: https://developers.openai.com/api/docs/guides/reasoning-best-practices
fetched: 2026-08-12
---

# OpenAI docs — Reasoning best practices (o-series vs GPT-series)

The doc that formally killed forced chain-of-thought for reasoning models.

## Planners vs workhorses
- **Reasoning models ("the planners")**: o-series (o3, o4-mini) "think longer and harder about complex tasks" — strategy, ambiguity, expert-accuracy domains (math, science, engineering, finance, law).
- **GPT models ("the workhorses")**: lower latency, cost-efficient, straightforward execution.
- > "An application might use o-series models to plan out the strategy to solve a problem, and use GPT models to execute specific tasks, particularly when speed and cost are more important than perfect accuracy."
- Combined pattern: "o-series for agentic planning and decision-making, GPT series for task execution."

## Prompting reasoning models — the reversal (quotable)
> "Since these models perform reasoning internally, prompting them to 'think step by step' or 'explain your reasoning' is unnecessary."
> — OpenAI, Reasoning best practices

(The page's bullet form is "Avoid chain-of-thought prompts" — the direct repudiation of 2023's #1 prompting technique.)

Other principles:
- Keep prompts "brief, clear" and direct — simple beats elaborate.
- Use delimiters (markdown, XML tags) to structure input.
- **"Try zero shot first, then few shot if needed"** — examples are a fallback, not a default. (Contrast: Anthropic docs' "Include 3–5 examples for best results" — see track2-vendor-disagreements.md.)
- Be specific about the end goal / success criteria; give explicit constraints.
- Use **developer messages** instead of system messages (as of o1-2024-12-17).

## When to pick which
Reasoning models when accuracy/reliability dominate and problems are complex and multistep; GPT models when speed and cost dominate and tasks are well-defined.
