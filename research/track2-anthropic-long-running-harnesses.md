---
url: https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
fetched: 2026-08-12
---

# Anthropic — "Effective harnesses for long-running agents" (Nov 26, 2025)

## What a harness solves
Discrete sessions: "each new session begins with no memory of what came before."

Framing metaphor (quotable):
> "Imagine a software project staffed by engineers working in shifts, where each new engineer arrives with no memory of what happened on the previous shift."
> — Anthropic, Effective harnesses for long-running agents

## The two-agent pattern
**Initializer agent** (first session): sets up environment — `init.sh` startup script, `claude-progress.txt` log, initial git commit, comprehensive JSON feature list (200+ items for a web app), all marked "failing".

**Coding agent** (every later session): one feature at a time; reads progress logs + git history; commits with descriptive messages; leaves the environment in a "clean state".

## Session ritual
`pwd` → read git logs and progress files → pick highest-priority incomplete feature → start dev server via script → run a basic end-to-end test *before* new work.

## Verification matters
> "Providing Claude with these kinds of testing tools dramatically improved performance, as the agent was able to identify and fix bugs." (browser automation for UI testing)

Guarding tests with strong wording: "It is unacceptable to remove or edit tests because this could lead to missing or buggy functionality."

## Open question stated in the post
> "it's still unclear whether a single, general-purpose coding agent performs best across contexts, or if better performance can be achieved through a multi-agent architecture."

## Note for the generation-shift story
This Nov-2025 post is deliberately era-bound: it prescribes heavy scaffolding (feature lists, rituals, strongly-worded rules) for *Sonnet 4.5-era* long-running work and does not claim permanence. Eight months later, the July 2026 new-rules post reports deleting much of exactly this kind of scaffolding for Claude 5-generation models — a clean before/after pair for slides.
