---
url: https://developers.openai.com/cookbook/examples/gpt-5/gpt-5_prompting_guide
url2: https://developers.openai.com/cookbook/examples/gpt-5/gpt-5-1_prompting_guide
url3: https://developers.openai.com/cookbook/examples/gpt-5/gpt-5-2_prompting_guide
fetched: 2026-08-12
---

# OpenAI Cookbook — GPT-5 / GPT-5.1 / GPT-5.2 Prompting Guides

As of 2026-08-12, GPT-5.2 is the latest general-model prompting guide in the cookbook (a Codex guide exists up to gpt-5.3-codex, out of scope here).

## GPT-5 guide (Aug 2025)
- **Agentic eagerness is a dial**, not a set of hardcoded reminders: reduce with lower `reasoning_effort` + stop criteria + tool budgets ("Switch to a lower reasoning_effort. This reduces exploration depth but improves efficiency and latency."); increase with persistence prompts ("Never stop or hand back to the user when you encounter uncertainty — research or deduce the most reasonable approach.").
- **Tool preambles**: prompt the model to "Always begin by rephrasing the user's goal in a friendly, clear, and concise manner, before calling any tools" — user-visible plan narration.
- **Responses API preserves reasoning across tool calls (quotable):** "we observed Tau-Bench Retail score increases from 73.9% to 78.2% just by switching to the Responses API."
- **Contradictions are now expensive (key quote):**
  > "poorly-constructed prompts containing contradictory or vague instructions can be more damaging to GPT-5 than to other models, as it expends reasoning tokens searching for a way to reconcile the contradictions."
  > — OpenAI, GPT-5 prompting guide
- `verbosity` API parameter decouples answer length from thinking depth.
- **Cursor's lesson** (old scaffolding backfires on new models): their context-maximization prompt "often caused the model to overuse tools by calling search repetitively, when internal knowledge would have been sufficient."
- Metaprompting: "several users have deployed prompt revisions to production that were generated simply by asking GPT-5 what elements could be added to an unsuccessful prompt to elicit a desired behavior."

## GPT-5.1 guide (Nov 2025)
- Adds `reasoning: none` mode — "functionally similar to GPT-4.1"; in that mode the old non-reasoning advice returns: "prompting the model to think carefully about which functions it plans to invoke can improve accuracy."
- Persistence still needs prompting: "Persist until the task is fully handled end-to-end within the current turn whenever feasible: do not stop at analysis or partial fixes." / "Be extremely biased for action."
- Instruction following is extremely literal: the model "will pay very close attention to the instructions you provide"; contradictions cause oscillation (e.g., "be concise" vs "err on completeness").
- **Prompt-hygiene doctrine (quotable):** "Prefer small, explicit edits: clarify conflicting rules, remove redundant or contradictory lines, tighten vague guidance."
- Migration from GPT-5: emphasize persistence; explicit length/structure rules; new apply_patch tool (35% fewer failures).

## GPT-5.2 guide (~Dec 2025/2026)
- Behavior deltas: "more deliberate scaffolding" in outputs, "generally lower verbosity" but "prompt-sensitive", "stronger instruction adherence", "conservative grounding bias."
- **Counterpoint to the thin-harness narrative:** OpenAI still prescribes explicit steering — "Implement EXACTLY and ONLY what the user requests. No extra features, no added components, no UX embellishments." And: "small changes to prompt structure, verbosity constraints, and reasoning settings often translate into large gains."
- Migration discipline: "Step 1: Switch models, don't change prompts yet." Then re-tune reasoning_effort (GPT-5.2 default is `none`, not `medium`). "Only soften or remove verbosity guidance if migration evals show unnecessary tightness."
- Long-horizon: `/responses/compact` endpoint for "loss-aware compression" — compact "after major milestones," not every turn; treat compacted items as "opaque; don't parse or depend on internals." (OpenAI's answer to Anthropic's server-side compaction.)
- Update cadence prompts: "Send brief updates (1–2 sentences) only when: You start a new major phase of work, or You discover something that changes the plan."

## Synthesis note
Across 5 → 5.1 → 5.2 OpenAI's arc is: fewer magic incantations, but MORE emphasis on prompt hygiene (contradiction removal) and explicit scope/verbosity constraints. OpenAI de-scaffolds by *cleaning* prompts; Anthropic de-scaffolds by *deleting* them. See track2-vendor-disagreements.md.
