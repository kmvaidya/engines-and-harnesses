---
url: https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-opus-5
url2: https://platform.claude.com/docs/en/about-claude/models/migration-guide
fetched: 2026-08-12
---

# Anthropic docs — "Prompting Claude Opus 5" + Migration guide

## The remove-your-scaffolding quote (strongest single migration line found)
> "Claude Opus 5 verifies its own work without being told to. If your prompt contains explicit verification instructions ('include a final verification step for any non-trivial task,' 'use a subagent to verify'), remove them: instructions like these cause over-verification on Claude Opus 5, and removing them reduces wasted tokens with no loss in quality. The same applies to legacy harness scaffolding that adds separate verification steps."
> — Anthropic, Prompting Claude Opus 5

Same logic for self-correction:
> "Avoid instructing re-checks it already performs ('double-check your answer,' 're-verify before responding'); like verification instructions, these compound with the model's own behavior and add cost without improving results."

## Literal instruction following cuts both ways
> "If your review prompt says 'only report high-severity issues' or 'be conservative,' the model may follow that instruction literally and report less; ask it to report everything and filter in a separate pass instead."

## Verbosity is now promptable, not parameter-controlled
"The effort parameter controls how much the model thinks rather than how much it says... To control response length, prompt for it explicitly." Written deliverables also run long — add length calibration.

## Subagent enthusiasm needs damping
> "Claude Opus 5 delegates to subagents more readily than prior models. Delegation pays off on genuinely independent, sizeable tracks of work, but it multiplies cost and time when applied to small tasks."
Sample damping prompt: "Do not delegate work you can finish yourself in a handful of tool calls, and do not use subagents to verify or double-check your own work."

## Vision workarounds obsolete
"Re-validate any prompt-side vision workarounds you tuned for prior models; they may no longer be needed."

## From the migration guide (verbatim highlights)
- "Claude Opus 5 verifies its own work without being told to, so remove explicit verification or self-check instructions carried over from prompts tuned for earlier models; leaving them in causes over-verification."
- "Claude Opus 4.7 provides more regular, higher-quality updates to the user throughout long agentic traces. If you've added scaffolding to force interim status messages ('After every 3 tool calls, summarize progress'), try removing it."
- "Claude Opus 4.7 has a tendency to use tools less often than Claude Opus 4.6 and to use reasoning more. This produces better results in most cases."
- Fable 5/Mythos 5: "Adaptive thinking is always on... Both `thinking: {type: \"disabled\"}` and manual extended thinking... return a 400 error."
- "Prefilling the assistant message returns a 400 error. Use system prompt instructions instead."
- Effort defaults: `high` is the default; "Lower effort settings still perform well and often exceed xhigh performance on prior models."

## Thinking-disabled edge cases (Opus 5)
With thinking disabled: occasional tool-calls-as-text and internal XML tag leakage. Counterintuitive fix: "If your system prompt contains a rule instructing the model not to think or not to reason, remove it; that kind of instruction increases tag leakage." And: "Instructions that call out thinking tags by name are less effective than the general form, so avoid naming them specifically."
