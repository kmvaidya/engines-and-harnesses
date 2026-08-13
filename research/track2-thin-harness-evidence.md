---
url: https://claude.com/blog/the-new-rules-of-context-engineering-for-claude-5-generation-models
url2: https://x.com/trq212/status/2080710971228918066
url3: https://simonwillison.net/2026/Jul/21/cat-and-thariq/
fetched: 2026-08-12
---

# The 80% claim: VERIFIED (with precise wording and caveats)

**Status: TRUE as stated, with one wording correction.** The claim under investigation — "Anthropic deleted over 80% of Claude Code's system prompt for Claude 5-generation models with no measurable loss" — is directly sourced to a primary Anthropic publication. The vendor's exact wording is "no measurable loss **on our coding evaluations**" (internal evals), not "no measurable loss" in general. Use the qualified form on slides.

## Primary source
- **Post:** "The new rules of context engineering for Claude 5 generation models," claude.com/blog, **July 24, 2026**, by **Thariq Shihipar, member of technical staff, Anthropic** (Claude Code team).
- **Exact quote:** "we removed over 80% of Claude Code's system prompt — and saw no measurable loss on our coding evaluations." (re: Claude Opus 5 and Claude Fable 5)
- **Announcement X post:** https://x.com/trq212/status/2080710971228918066 (@trq212)
- **Supporting appearance:** fireside chat with Cat and Thariq of the Claude Code team, July 21, 2026, written up by Simon Willison (simonwillison.net/2026/Jul/21/cat-and-thariq/; video: youtube.com/watch?v=uU5Gv2h8-9g). Also referenced in talks around the AI Engineer World's Fair.

## What was actually deleted (the six shifts, per the primary post)
1. Rules → judgment ("Write code that reads like the surrounding code: match its comment density, naming, and idiom.")
2. Examples → interface design ("giving examples actually constrains them to a certain exploration space")
3. Everything upfront → progressive disclosure (skills, deferred tool-definition loading)
4. Duplicated instructions → consolidated into tool descriptions
5. Manual CLAUDE.md memory (# hotkey) → auto-memory
6. Simple markdown specs → rich references (HTML artifacts, test suites, code)

## Why (their stated mechanism)
- "We found that we were overconstraining Claude Code, both through our system prompt and in our CLAUDE.md files and skills." Example of self-contradiction inside the old prompt: "default to writing no comments" alongside "never write multi-paragraph docstrings or multi-line comment blocks — one short line max."
- "Claude must think more carefully about these overlapping and conflicting messages before deciding what to do."
- "we have since found we can delete many of them and let the model use surrounding context and judgement instead."
- Fireside-chat color: Cat — many instructions were only "90% true" with edge cases; Thariq — "removing examples was extremely helpful, because it was just more creative than the examples we gave it."

## Caveats to disclose
1. **Self-reported**: 80% is Anthropic's own measurement on Anthropic's own internal coding evals; no public breakdown of which task categories held vs softened, and no third-party replication.
2. **Model-gated**: per the fireside chat, Claude Code maintains "a different system prompt per model" — the lean prompt ships only to frontier models (Fable 5 / Opus 5 / Opus 4.8-class); older models keep the full prompt "because they lack sufficient judgment for flexible instructions."
3. **Percentage of what**: the post does not publish absolute before/after token counts for the full Claude Code prompt. Third-party trackers (e.g., github.com/Piebald-AI/claude-code-system-prompts, which snapshots every Claude Code version's prompts) are the best independent way to verify magnitude. Some low-quality aggregator coverage circulates garbled numbers ("800 tokens to 164") — do not use those.

## Corroborating vendor evidence that harnesses thin as models improve (all verifiable, all vendor-authored)
- **Anthropic, Fable 5 docs:** "Skills developed for prior models are often too prescriptive for Claude Fable 5 and can degrade output quality. Review and consider removing older instructions if default performance is better." — platform.claude.com/docs/.../prompting-claude-fable-5
- **Anthropic, Opus 5 docs:** "remove them: instructions like these cause over-verification on Claude Opus 5, and removing them reduces wasted tokens with no loss in quality." — platform.claude.com/docs/.../prompting-claude-opus-5
- **Anthropic, best-practices docs:** "Where you might have said 'CRITICAL: You MUST use this tool when...', you can use more normal prompting like 'Use this tool when...'." — platform.claude.com/docs/.../claude-prompting-best-practices
- **Anthropic, migration guide:** "If you've added scaffolding to force interim status messages ('After every 3 tool calls, summarize progress'), try removing it." — platform.claude.com/docs/en/about-claude/models/migration-guide
- **Anthropic, API deprecations as forced de-scaffolding:** prefills return 400 ("Model intelligence and instruction following have advanced such that most use cases of prefill no longer require it."); `budget_tokens` removed in favor of adaptive thinking.
- **Anthropic, context engineering post (Sep 2025) predicted it:** "smarter models require less prescriptive engineering, allowing agents to operate with more autonomy." — anthropic.com/engineering/effective-context-engineering-for-ai-agents
- **OpenAI, reasoning best practices:** the deprecation of prompt tricks in doctrine form — "Since these models perform reasoning internally, prompting them to 'think step by step' or 'explain your reasoning' is unnecessary." Plus "Try zero shot first, then few shot if needed."
- **OpenAI, GPT-5 guide (Cursor case study):** old scaffolding actively harmed the new model — the context-maximization prompt "often caused the model to overuse tools by calling search repetitively, when internal knowledge would have been sufficient."
- **OpenAI, GPT-5.1 guide:** prompt slimming as hygiene — "Prefer small, explicit edits: clarify conflicting rules, remove redundant or contradictory lines, tighten vague guidance."
- **Counterweight (include for balance):** OpenAI's GPT-5.2 guide still leans on explicit steering ("Implement EXACTLY and ONLY what the user requests...") and advises "Switch models, don't change prompts yet" — the thinning trend is real but not uniform across labs or model lines.

## One-line verdict for the deck
The 80% claim is real, primary-sourced, and precisely dated (Anthropic, Jul 24, 2026) — but it is Anthropic grading its own homework on internal evals, applies only to Claude 5-generation models, and the same team keeps the fat prompt in production for older models.
