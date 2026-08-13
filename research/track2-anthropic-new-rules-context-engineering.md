---
url: https://claude.com/blog/the-new-rules-of-context-engineering-for-claude-5-generation-models
url2: https://x.com/trq212/status/2080710971228918066
fetched: 2026-08-12
---

# Anthropic — "The new rules of context engineering for Claude 5 generation models" (Jul 24, 2026)

Author: **Thariq Shihipar, member of technical staff, Anthropic** (Claude Code team). Announced via X post @trq212; discussed at the AI Engineer World's Fair and in a July 21, 2026 fireside chat covered by Simon Willison.

## THE headline claim (primary source for the 80% story)
> "we removed over 80% of Claude Code's system prompt — and saw no measurable loss on our coding evaluations."
> — Thariq Shihipar, Anthropic (claude.com/blog, Jul 24, 2026), re: Claude Opus 5 / Claude Fable 5

## Why the old prompt hurt
> "We found that we were overconstraining Claude Code, both through our system prompt and in our CLAUDE.md files and skills."

Conflicting rules stacked up (e.g., the system prompt simultaneously prescribed "default to writing no comments" and "never write multi-paragraph docstrings or multi-line comment blocks — one short line max"):
> "Claude must think more carefully about these overlapping and conflicting messages before deciding what to do."

> "we have since found we can delete many of them and let the model use surrounding context and judgement instead."

## The six shifts (then → now)
1. **Rules → Judgment.** Replace rule lists with intent: "Write code that reads like the surrounding code: match its comment density, naming, and idiom."
2. **Examples → Interface design.** "giving examples actually constrains them to a certain exploration space" — design expressive tool parameters instead of few-shot walls.
3. **Everything upfront → Progressive disclosure.** Verification/code-review guidance moved out of the system prompt into optional skills; deferred loading of tool definitions (Claude searches definitions when needed).
4. **Repeated instructions → Simple tool descriptions.** Kill duplication between system prompt and tool descriptions; guidance lives in the tool definition.
5. **Manual memory (CLAUDE.md `#` hotkey) → Auto-memory.** "Claude now automatically saves memories that are relevant to the work."
6. **Simple specs → Rich references.** Markdown specs replaced by higher-fidelity references: HTML artifacts, "detailed test suites, or a function in a different codebase." Related guidance: prefer "files that are in code as they provide clear, high-fidelity instructions to Claude in a language it knows very well."

## Practical context-assembly guidance
- System prompt: "heavily tied to the product context. It tells Claude what product it's operating in."
- CLAUDE.md: "Keep your CLAUDE.md lightweight... spend most of the tokens on gotchas inside of the codebase."
- Skills: "Think of skills as lightweight guides... Avoid making them overconstrained, except in highly important areas."
- Closing: "Across your system prompt, skills, and CLAUDE.md files, you may need to simplify just like we did." (`/doctor` in Claude Code automates the audit.)

## Corroborating color from the Jul 21 fireside chat (via simonwillison.net/2026/Jul/21/cat-and-thariq/)
- Thariq: "removing examples was extremely helpful, because it was just more creative than the examples we gave it."
- Cat: many instructions were only "90% true" with problematic edge cases → shift from absolute constraints to contextual guidance.
- They maintain "a different system prompt per model" — only frontier models (Fable, Opus 4.8+) get the lean prompt; older models keep the full one because they lack the judgment for flexible instructions.
- "fewer 'do not do this' instructions" — prohibition lists confuse more than help.

## Caveats to state honestly on slides
- 80% is Anthropic's own number, on Anthropic's own internal coding evals; no public breakdown of which task categories held or softened.
- Applies to Claude 5-generation models only; the fat prompt still ships to older models (per the fireside chat).
