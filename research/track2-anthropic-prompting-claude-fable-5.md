---
url: https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-fable-5
fetched: 2026-08-12
---

# Anthropic docs — "Prompting Claude Fable 5" (frontier-model page, Claude 5 generation)

The clearest official statement that a capability jump should trigger a *scaffolding audit*:

> "Capability improvements at this level are also a good prompt to re-evaluate which instructions, tools, and guardrails are still needed."
> — Anthropic, Prompting Claude Fable 5

## Capability deltas vs Opus 4.8 (paraphrase)
Long-horizon autonomy ("completing multiday, goal-directed runs"); first-shot correctness ("Early testers reported single-pass implementations of systems that previously took days of iteration"); vision; enterprise workflows; code review; ambiguity navigation; "significantly more dependable at dispatching and sustaining parallel subagents."

Positioning: "The teams seeing the best outcomes apply Claude Fable 5 to their hardest unsolved problems; testing it only on simpler workloads tends to undersell its capability range."

## Strong instruction following — brevity replaces enumeration (quotable)
> "Instruction-following is improved enough that you can steer most behaviors with a brief instruction rather than enumerating each behavior by name."

Same for checkpoints: "To have Claude Fable 5 stop only where it genuinely needs you, there is no need to enumerate every case."

## De-scaffolding guidance (key generation-shift evidence)
> "Refactor existing prompts and skills. Skills developed for prior models are often too prescriptive for Claude Fable 5 and can degrade output quality. Review and consider removing older instructions if default performance is better."
> — Anthropic, Prompting Claude Fable 5 (Recommended scaffolding changes)

Also: "Claude Fable 5 also does a good job of updating skills on the fly based on what it learns from the task at hand."

## Grounded progress claims
> "Before reporting progress, audit each claim against a tool result from this session." — sample prompt; "In Anthropic's testing, this nearly eliminated fabricated status reports even on tasks designed to elicit them."

## Memory doctrine
> "Claude Fable 5 performs particularly well when it can record lessons from previous runs and reference them. Provide a place to write notes, as simple as a Markdown file."
Sample: one lesson per file, one-line summary at top, delete wrong notes; bootstrap memory by having the model review past sessions with subagents.

## Other operational notes
- Longer turns by default: "Individual requests on hard tasks can run for many minutes at higher effort settings... autonomous runs can extend for hours." Restructure harnesses to check asynchronously rather than blocking.
- Effort is "the primary control for the trade-off between intelligence, latency, and cost"; "Lower effort settings on Claude Fable 5 still perform well and often exceed xhigh performance on prior models."
- Parallel subagents: "dispatches parallel subagents more readily than prior models. Use subagents frequently... prefer asynchronous communication."
- Verification: "Separate, fresh-context verifier subagents tend to outperform self-critique."
- Context-budget anxiety: avoid showing remaining-token countdowns; reassure "You have ample context remaining."
- Give the reason, not only the request: "Claude Fable 5 tends to perform better when it understands the intent behind a request."
- Don't ask the model to echo its reasoning (triggers `reasoning_extraction` refusals) — read structured thinking blocks instead; add a `send_to_user` tool for verbatim mid-run messages.
