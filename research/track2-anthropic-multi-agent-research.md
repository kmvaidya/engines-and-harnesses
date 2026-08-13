---
url: https://www.anthropic.com/engineering/multi-agent-research-system
fetched: 2026-08-12
---

# Anthropic — "How we built our multi-agent research system" (Jun 13, 2025)

## The headline number
> "a multi-agent system with Claude Opus 4 as the lead agent and Claude Sonnet 4 subagents outperformed single-agent Claude Opus 4 by 90.2%" (internal research eval)
> — Anthropic, Multi-agent research system

## Why multi-agent works for research
> "Research demands the flexibility to pivot or explore tangential connections as the investigation unfolds."

Parallel subagents = separate context windows = more total tokens applied to the problem:
> "token usage by itself explains 80% of the variance, with the number of tool calls and the model choice as the two other explanatory factors." (three factors together explained 95% of variance)

## Architecture
Orchestrator-worker: lead agent plans strategy, spawns parallel specialized subagents, synthesizes, decides whether more research is needed.

## Prompt-engineering lessons for multi-agent
1. Teach the orchestrator to delegate: "Each subagent needs an objective, an output format, guidance on the tools and sources to use, and clear task boundaries." Vague instructions → duplication and gaps.
2. Scale effort to complexity: simple query = 1 agent / 3–10 calls; complex = 10+ subagents with divided responsibilities.
3. Let the model improve its own prompts: Claude diagnosing prompt failures → 40% faster task completion.
4. Parallel tool calling: "These changes cut research time by up to 90% for complex queries."

## The honest cost accounting (quotable)
> "agents typically use about 4× more tokens than chat interactions, and multi-agent systems use about 15× more tokens than chats."
> — Anthropic, Multi-agent research system

Early failure modes: spawning 50 subagents for simple queries; endless searching for nonexistent sources.

## When NOT to use multi-agent
> "most coding tasks involve fewer truly parallelizable tasks than research"

Bad fit: domains needing shared context or with dense interdependencies. Good fit: heavy parallelization, information beyond one context window, complex tool surfaces.
