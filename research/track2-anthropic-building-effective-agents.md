---
url: https://www.anthropic.com/engineering/building-effective-agents
fetched: 2026-08-12
---

# Anthropic — "Building effective agents" (Dec 19, 2024)

The foundational agents-doctrine post. Still the canonical Anthropic statement on simplicity over frameworks.

## Core definitions
- **Workflows**: "systems where LLMs and tools are orchestrated through predefined code paths"
- **Agents**: "systems where LLMs dynamically direct their own processes and tool usage"

## Quotable — simplicity doctrine
> "the most successful implementations weren't using complex frameworks or specialized libraries. Instead, they were building with simple, composable patterns"
> — Anthropic, Building effective agents (Dec 2024)

> "Success in the LLM space isn't about building the most sophisticated system."
> — Anthropic, Building effective agents

On frameworks:
> "ensure you understand the underlying code. Incorrect assumptions about what's under the hood are a common source of customer error"
> — Anthropic, Building effective agents

## Five workflow patterns
1. Prompt chaining — sequential decomposition with programmatic gates
2. Routing — classify input, dispatch to specialized downstream tasks
3. Parallelization — sectioning or voting
4. Orchestrator-workers — dynamic subtask delegation + synthesis
5. Evaluator-optimizer — iterate via evaluation feedback loops

## When to use agents
Open-ended problems where steps can't be predicted, extended autonomous operation, and enough trust/oversight. Costs: higher token spend and compounding-error risk.

## Three core principles
1. **Simplicity** in design
2. **Transparency** — show the agent's planning explicitly
3. **A well-crafted agent-computer interface (ACI)** — tool documentation and testing

## Slide relevance
This Dec-2024 doctrine ("simple, composable patterns" beat frameworks) is the seed of the 2026 "thin harness" position — the argument was made *before* reasoning-era models made it even more true.
