---
url: https://cdn.openai.com/business-guides-and-resources/a-practical-guide-to-building-agents.pdf
url2: https://openai.github.io/openai-agents-python/
fetched: 2026-08-12
---

# OpenAI — "A practical guide to building agents" (PDF, 2025) + Agents SDK philosophy

Read from the live PDF (34 pp). OpenAI's canonical agent-architecture doctrine.

## Definition (quotable)
> "Agents are systems that independently accomplish tasks on your behalf."
> — OpenAI, A practical guide to building agents

> "Applications that integrate LLMs but don't use them to control workflow execution—think simple chatbots, single-turn LLMs, or sentiment classifiers—are not agents."

## When to build one
Prioritize workflows resisting automation: (1) complex decision-making, (2) difficult-to-maintain rules ("Systems that have become unwieldy due to extensive and intricate rulesets"), (3) heavy reliance on unstructured data. "Otherwise, a deterministic solution may suffice."

## Three components
Model (reasoning/decisions) + Tools (data / action / orchestration — "Agents themselves can serve as tools for other agents") + Instructions.

## Model selection
Prototype with the most capable model to set a baseline, then swap in smaller models where results hold. Principles: set up evals; hit accuracy targets with the best models; then optimize cost/latency.

## Instructions
Use existing operating procedures; break down tasks; "Define clear actions"; capture edge cases with conditional branches. Use advanced models to auto-convert help-center docs into agent routines.

## Orchestration — the incrementalism doctrine (key quotes)
> "While it's tempting to immediately build a fully autonomous agent with complex architecture, customers typically achieve greater success with an incremental approach."

> "Our general recommendation is to maximize a single agent's capabilities first. More agents can provide intuitive separation of concepts, but can introduce additional complexity and overhead, so often a single agent with tools is sufficient."
> — OpenAI, A practical guide to building agents

- The loop is the unit: "Every orchestration approach needs the concept of a 'run', typically implemented as a loop that lets agents operate until an exit condition is reached."
- Prompt templates with policy variables as the anti-complexity move before going multi-agent.
- Split only on: **complex logic** (too many if-then-else branches in prompts) or **tool overload** — "Some implementations successfully manage more than 15 well-defined, distinct tools while others struggle with fewer than 10 overlapping tools."
- Two multi-agent patterns: **Manager (agents as tools)** and **Decentralized (agents handing off to agents)**.
- "Regardless of the orchestration pattern, the same principles apply: keep components flexible, composable, and driven by clear, well-structured prompts."
- Framework skepticism aimed at declarative graphs: they "can quickly become cumbersome and challenging as workflows grow more dynamic and complex, often necessitating the learning of specialized domain-specific languages" — vs. the SDK's "more flexible, code-first approach."

## Agents SDK design philosophy (openai.github.io/openai-agents-python)
- Two design principles: "Enough features to be worth using, but few enough primitives to make it quick to learn." and "Works great out of the box, but you can customize exactly what happens."
- Minimal primitives: Agents ("LLMs equipped with instructions and tools"), Handoffs ("delegate to other agents for specific tasks"), Guardrails, Sessions.
- "a production-ready upgrade of our previous experimentation for agents, Swarm"; "a built-in loop that continues until the task is complete."

## Slide relevance
OpenAI's own agent doctrine is remarkably close to Anthropic's Building Effective Agents on the core point: simple loop first, minimal abstraction, multi-agent only when a single agent demonstrably fails. The residual difference is that OpenAI ships an SDK with handoff primitives while Anthropic tells you to write the loop yourself — see track2-vendor-disagreements.md.
