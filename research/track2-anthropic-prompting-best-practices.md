---
url: https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices
fetched: 2026-08-12
---

# Anthropic docs — "Prompting best practices" (consolidated reference, Claude 5 era)

**Structural fact worth a slide by itself:** the old separate technique pages (be-clear-and-direct, multishot-prompting, chain-of-thought, use-xml-tags, system-prompts/role, long-context-tips, extended-thinking-tips, claude-4-best-practices) now all redirect to this ONE consolidated page. docs.claude.com itself redirects to platform.claude.com. The page covers "Claude Fable 5, Claude Mythos 5, Claude Opus 5, Claude Opus 4.8, Claude Opus 4.7, Claude Opus 4.6, Claude Sonnet 5, Claude Sonnet 4.6, and Claude Haiku 4.5" and is organized: model-specific guidance first, general techniques second, "Migration considerations last, for prompts moving from earlier generations."

## General principles (still standing across generations)
- **Be clear and direct:** "Claude responds well to clear, explicit instructions." / "If you want 'above and beyond' behavior, explicitly request it rather than relying on the model to infer this from vague prompts."
- New-employee framing: "Think of Claude as a brilliant but new employee who lacks context on your norms and workflows."
- **Golden rule (quotable):** "Show your prompt to a colleague with minimal context on the task and ask them to follow it. If they'd be confused, Claude will be too."
- **Motivation beats prohibition:** less effective: "NEVER use ellipses"; more effective: "Your response will be read aloud by a text-to-speech engine, so never use ellipses since the text-to-speech engine will not know how to pronounce them." Then: "Claude is smart enough to generalize from the explanation."
- **Examples:** "Examples are one of the most reliable ways to steer Claude's output format, tone, and structure." Advice: relevant, diverse, wrapped in `<example>` tags; "Include 3–5 examples for best results." (NOTE the tension with the Claude Code team's finding that removing examples helped Claude 5 models — see track2-thin-harness-evidence.md.)
- **XML tags:** "XML tags help Claude parse complex prompts unambiguously" — `<instructions>`, `<context>`, `<input>`.
- **Role prompting:** a single system-prompt sentence still "focuses Claude's behavior and tone".
- **Long context:** longform data at the TOP, query at the end — "Queries at the end can improve response quality by up to 30 percent in tests"; wrap documents in `<document>` tags; ask for grounding quotes first.

## Tool use — the de-escalation quote (key generation-shift evidence)
> "Claude Opus 4.5 and Claude Opus 4.6 are also more responsive to the system prompt than previous models. If your prompts were designed to reduce undertriggering on tools or skills, these models may now overtrigger. The fix is to dial back any aggressive language. Where you might have said 'CRITICAL: You MUST use this tool when...', you can use more normal prompting like 'Use this tool when...'."
> — Anthropic, Prompting best practices

Also: `<default_to_action>` vs `<do_not_act_before_instructions>` sample prompts; parallel tool calling is near-default and steerable to ~100%.

## Thinking and reasoning
- Claude 4.6+ / Fable 5: **adaptive thinking** ("thinking is always on" for Fable 5/Mythos 5); `budget_tokens` deprecated → 400 error on 4.7+; control via `effort`.
- "In internal evaluations, adaptive thinking reliably drives better performance than extended thinking."
- **Prefer general instructions over prescriptive steps (quotable):** "A prompt like 'think thoroughly' often produces better reasoning than a hand-written step-by-step plan. Claude's reasoning frequently exceeds what a human would prescribe."
- Manual CoT is now a **fallback** "when thinking is off", not the default technique.
- Self-check instructions: useful — EXCEPT "Claude Opus 5 is the exception: it verifies its own work well without explicit instruction, and verification instructions carried over from prompts tuned for earlier models can cause over-verification... When migrating to Claude Opus 5, remove these instructions rather than rewriting them."
- Overthinking on Opus 4.6: "Remove over-prompting. Tools that undertriggered in previous models are likely to trigger appropriately now. Instructions like 'If in doubt, use [tool]' will cause overtriggering."

## Agentic systems
- Context awareness (Sonnet 4.5+): model tracks its own remaining token budget; prompt it about compaction so it doesn't wrap up early.
- Multi-window workflows: different prompt for first window (setup: tests, init.sh); "Claude's latest models are extremely effective at discovering state from the local filesystem. In some cases, you may want to take advantage of this over compaction."
- Subagent orchestration: "Claude's latest models orchestrate subagents natively... proactively without requiring explicit instruction." Watch for overuse: "Claude Opus 4.6 has a strong predilection for subagents and may spawn them in situations where a simpler, direct approach would suffice."
- Prompt chaining is demoted: "With adaptive thinking and subagent orchestration, Claude handles most multistep reasoning internally." Chaining survives mainly for inspectable pipelines/self-correction.
- Overeagerness/overengineering: sample prompt telling the model NOT to add features, docstrings, defensive code, or abstractions ("The right amount of complexity is the minimum needed for the current task.")

## Prefill deprecation (hard API evidence of technique obsolescence)
> "Starting with Claude 4.6 models and Claude Mythos Preview, prefilled responses... are no longer supported. Requests with prefilled assistant messages to these models return a 400 error. Model intelligence and instruction following have advanced such that most use cases of prefill no longer require it."

Migrations: structured outputs for format forcing; direct instructions for preamble-stripping; "Claude is much better at appropriate refusals now."

## Migration considerations (verbatim highlights)
1. "Be specific about desired behavior"
2. Use quality modifiers ("Go beyond the basics to create a fully-featured implementation.")
3. Request features (animations etc.) explicitly
4. Adaptive thinking replaces budget_tokens
5. Migrate off prefills
6. **"Tune anti-laziness prompting: If your prompts previously encouraged the model to be more thorough or use tools more aggressively, dial back that guidance. Claude 4.6 models are more proactive and may overtrigger on instructions that were needed for previous models."**
