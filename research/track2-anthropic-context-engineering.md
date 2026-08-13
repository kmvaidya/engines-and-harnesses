---
url: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
fetched: 2026-08-12
---

# Anthropic — "Effective context engineering for AI agents" (Sep 29, 2025)

The post that reframed the discipline: prompt engineering is a subset of context engineering.

## Definition shift
- Prompt engineering = "writing and organizing LLM instructions for optimal outcomes"
- Context engineering = "the set of strategies for curating and maintaining the optimal set of tokens (information) during LLM inference"
- Prompt engineering is a discrete act; context engineering is **iterative** — curation happens at every inference cycle.

## Quotable — attention budget & context rot
> "Context, therefore, must be treated as a finite resource with diminishing marginal returns."
> — Anthropic, Effective context engineering for AI agents

> "as the number of tokens in the context window increases, the model's ability to accurately recall information from that context decreases." (defining "context rot")
> — Anthropic, Effective context engineering for AI agents

Mechanism claim: transformer attention has n² pairwise token relationships; longer contexts stretch the attention budget thin.

## The "right altitude" for system prompts
Two failure modes:
- Too specific: hardcoded, brittle if-else prompt logic
- Too vague: high-level guidance with no grounding

The ideal is "specific enough to guide behavior effectively, yet flexible enough to provide the model with strong heuristics to guide behavior."

## Just-in-time retrieval
Agents keep "lightweight identifiers (file paths, stored queries, web links, etc.) and use these references to dynamically load data into context at runtime using tools" — mirroring how humans retrieve rather than memorize. Tradeoff: "runtime exploration is slower than retrieving pre-computed data" — hybrid (some upfront + autonomous exploration) often wins.

## Long-horizon techniques (the canonical trio)
1. **Compaction** — summarize and reinitialize near the context limit; art = keep architectural decisions/bugs, drop redundant tool outputs.
2. **Structured note-taking** — external memory files (NOTES.md, to-do lists) give "persistent memory with minimal overhead".
3. **Sub-agent architectures** — clean-context specialists return condensed summaries (1,000–2,000 tokens) to an orchestrator; "clear separation of concerns."

## Quotable — the generation-shift line
> "smarter models require less prescriptive engineering, allowing agents to operate with more autonomy."
> — Anthropic, Effective context engineering for AI agents

But the constraint persists:
> "treating context as a precious, finite resource will remain central to building reliable, effective agents."

Closing guidance: **"do the simplest thing that works."**
