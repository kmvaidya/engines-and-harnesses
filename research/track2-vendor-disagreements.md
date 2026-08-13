---
url: (synthesis — both sides quoted with vendor URLs inline)
fetched: 2026-08-12
---

# Where Anthropic and OpenAI disagree (or visibly diverge)

Genuine head-to-head disagreements are rarer than the discourse suggests — on agent simplicity the two labs nearly quote each other. Below: real divergences, each with both sides quoted.

## 1. Few-shot examples for frontier models
- **Anthropic (docs, general guidance):** "Examples are one of the most reliable ways to steer Claude's output format, tone, and structure... Include 3–5 examples for best results." — platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices. Even for thinking models: "Multishot examples work with thinking. Use `<thinking>` tags inside your few-shot examples to show Claude the reasoning pattern."
- **Anthropic (Claude Code team, frontier practice):** "giving examples actually constrains them to a certain exploration space" (claude.com/blog/the-new-rules-of-context-engineering-for-claude-5-generation-models); "removing examples was extremely helpful, because it was just more creative than the examples we gave it" (Thariq, via simonwillison.net/2026/Jul/21/cat-and-thariq/).
- **OpenAI (reasoning models):** "Try zero shot first, then few shot if needed." — developers.openai.com/api/docs/guides/reasoning-best-practices
- Verdict: this is as much an *intra-Anthropic* tension (docs vs frontier team) as an inter-vendor one. OpenAI's zero-shot-first line and Anthropic's frontier practice agree; Anthropic's general docs lag.

## 2. XML vs markdown as prompt structure
- **Anthropic:** XML-native. "XML tags help Claude parse complex prompts unambiguously" — wrap instructions/context/examples in tags; document sets in `<document>` trees; even output steering via XML format indicators. — platform.claude.com/docs/.../claude-prompting-best-practices
- **OpenAI:** markdown-first, XML situational. GPT-4.1 guide: start with markdown H1–H4 sections; but for large document collections "XML and pipe-delimited formats outperformed JSON significantly in testing." — developers.openai.com/cookbook/examples/gpt4-1_prompting_guide. (GPT-5.2-era commentary keeps "XML scaffolding for agents" as a technique, not a default.)
- Verdict: real but mild — house styles, both endorse delimiters; the shared enemy is JSON-as-prompt-structure.

## 3. Multi-agent: force multiplier vs last resort
- **Anthropic:** built and champions an orchestrator-worker research system: "a multi-agent system... outperformed single-agent Claude Opus 4 by 90.2%" — anthropic.com/engineering/multi-agent-research-system. Claude 5-era models are trained INTO delegation: "Claude's latest models orchestrate subagents natively... proactively without requiring explicit instruction" (docs); Fable 5 "dispatches parallel subagents more readily than prior models. Use subagents frequently" (prompting-claude-fable-5). Anthropic's caveats: 15× token cost, and "most coding tasks involve fewer truly parallelizable tasks than research."
- **OpenAI:** "Our general recommendation is to maximize a single agent's capabilities first. More agents can provide intuitive separation of concepts, but can introduce additional complexity and overhead, so often a single agent with tools is sufficient." — cdn.openai.com/business-guides-and-resources/a-practical-guide-to-building-agents.pdf
- Verdict: sharpest real divergence in emphasis. Anthropic now treats delegation as a first-class model capability (needing damping prompts!); OpenAI treats multi-agent as an escalation you earn after single-agent failure.

## 4. Agent abstractions: SDK primitives vs raw loop
- **OpenAI:** ships opinionated primitives — Agents SDK with handoffs/guardrails/sessions, "a production-ready upgrade of... Swarm", "Enough features to be worth using, but few enough primitives to make it quick to learn." — openai.github.io/openai-agents-python
- **Anthropic:** framework-skeptical: "the most successful implementations weren't using complex frameworks or specialized libraries. Instead, they were building with simple, composable patterns" and if you use a framework, "ensure you understand the underlying code." — anthropic.com/engineering/building-effective-agents
- Verdict: both preach simplicity; OpenAI productizes it, Anthropic tells you to own the loop. Note OpenAI's own guide also jabs at declarative graph frameworks ("cumbersome... specialized domain-specific languages"), so the disagreement is Anthropic-vs-SDKs generally, softened by OpenAI's minimalism.

## 5. Does the frontier model need MORE steering or LESS?
- **Anthropic (July 2026):** less. "we removed over 80% of Claude Code's system prompt — and saw no measurable loss on our coding evaluations"; "delete many of them and let the model use surrounding context and judgement instead." — claude.com/blog/the-new-rules-of-context-engineering-for-claude-5-generation-models
- **OpenAI (GPT-5.2 guide):** still explicit-steering-heavy: "Implement EXACTLY and ONLY what the user requests. No extra features, no added components, no UX embellishments."; "small changes to prompt structure, verbosity constraints, and reasoning settings often translate into large gains." Migration doctrine: "Step 1: Switch models, don't change prompts yet." — developers.openai.com/cookbook/examples/gpt-5/gpt-5-2_prompting_guide
- Verdict: philosophical split on migration mechanics: Anthropic says audit-and-delete ("you may need to simplify just like we did"); OpenAI says freeze-then-tune. Both converge on removing *contradictions* ("remove redundant or contradictory lines" — GPT-5.1 guide).

## 6. Where they agree so hard it's boring (use as the punchline)
- Contradictions are the new prompt bug: OpenAI "expends reasoning tokens searching for a way to reconcile the contradictions" ≈ Anthropic "Claude must think more carefully about these overlapping and conflicting messages before deciding what to do."
- Empiricism: OpenAI "AI engineering is inherently an empirical discipline" ≈ Anthropic's evals-before-prompting stance (prompt-engineering overview).
- Simplicity: Anthropic "do the simplest thing that works" ≈ OpenAI "customers typically achieve greater success with an incremental approach."
