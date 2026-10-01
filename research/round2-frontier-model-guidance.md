---
url: https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-fable-5, https://developers.openai.com/api/docs/guides/prompt-guidance.md, https://developers.openai.com/api/docs/changelog.md, https://ai.google.dev/gemini-api/docs/models, https://ai.google.dev/gemini-api/docs/latest-model, https://ai.google.dev/gemini-api/docs/gemini-3, https://ai.google.dev/gemini-api/docs/whats-new-gemini-3.5, https://ai.google.dev/gemini-api/docs/thinking, https://ai.google.dev/gemini-api/docs/prompting-strategies, https://ai.google.dev/gemini-api/docs/function-calling, https://ai.google.dev/gemini-api/docs/caching, https://ai.google.dev/gemini-api/docs/long-context, https://ai.google.dev/gemini-api/docs/computer-use
fetched: 2026-09-30
---

# Frontier-model guidance that affects harness design (Sep 2026)

Round 2 file. Tags: **[V]** 3-agent adversarial check passed, **[S]** hand
spot-check, **[P]** confirmed against the primary source on 2026-09-30,
**[E]** extracted with quote but not cross-checked, **[R]** refuted.

Both sources are vendor documentation. The behaviours they describe ("nearly
eliminated fabricated status reports", longer turns) have no published method
or numbers and no independent check.

Gemini 3.x guidance was added in a follow-up pass on 2026-09-30 (§4).

## 1. Anthropic: Claude Fable 5 guide (live on 2026-09-30)

Round 1 (`track2-anthropic-prompting-claude-fable-5.md`) captured the "older
skills are too prescriptive" point. These items are new or newly recorded.
Scope: Fable 5 and Mythos 5, mostly long autonomous runs.

- **Much longer turns** [V]. "Individual requests on hard tasks can run for
  many minutes at higher effort settings ... and autonomous runs can extend
  for hours. This is one of the largest shifts teams encounter ... Adjust
  client timeouts, streaming, and user-facing progress indicators before
  migrating, and consider restructuring harnesses to check on runs
  asynchronously, for example through scheduled jobs, rather than blocking."
- **Grounded progress reports** [V]. Telling the model to check each progress
  claim against tool results from the session "nearly eliminated fabricated
  status reports even on tasks designed to elicit them."
- **Verifier subagents** [V]. "Separate, fresh-context verifier subagents tend
  to outperform self-critique."
- **Old skills hurt** [V]. "Skills developed for prior models are often too
  prescriptive for Claude Fable 5 and can degrade output quality."
- **reasoning_extraction refusal** [V]. Prompts, skills or harness
  instructions that tell the model to echo, transcribe or explain its internal
  reasoning as response text can trigger this refusal category. Server-side
  fallback with `fallbacks: "default"` does not retry it.
- **Do not show a token countdown** [P]. Under "Rare cases of context-budget
  concern", the model may "suggest a new session, offer to summarize and hand
  off, or trim its own work". "This is most often triggered when the harness
  shows a remaining-token countdown to the model. Avoid surfacing explicit
  context-budget counts where possible." If counts must be shown, the guide
  suggests adding reassurance text. Early stopping is a separate section and
  is not tied to token counts; round 2 originally conflated the two.
- **Memory** [P]. "Provide a place to write notes, as simple as a Markdown
  file". The guide's sample prompt says: "Store one lesson per file with a
  one-line summary at the top."
- **send_to_user tool** [P]. "Defining the tool is not sufficient on its own;
  without an instruction in the system prompt, Claude Fable 5 rarely calls it."
- **Effort is the main dial** [P]. "Use `high` as the default for most tasks,
  with `xhigh` for the most capability-sensitive workloads and `medium` or
  `low` for routine work. Lower effort settings on Claude Fable 5 still
  perform well and often exceed `xhigh` performance on prior models."
  Adaptive thinking only; no extended thinking budgets.
- **Safety classifiers** [P]. Three categories: offensive cybersecurity
  techniques, biology and life sciences content, and extraction of the
  model's summarized thinking. Benign requests "may also trigger these
  safeguards". "To re-route declined requests automatically, configure
  server-side or client-side fallback to Claude Opus 4.8." Relevant to bank
  security teams using agents on security tooling.

## 2. OpenAI: the GPT-6 family

**Change since round 1** [V]. The URL that served the GPT-5.x prompt guide now
serves "Using GPT-6". Round 1's `track2-openai-gpt5-prompting-guides.md` is the
previous generation.

- Models [P] (developers.openai.com changelog and model pages): four model
  IDs, not an inconsistent name. `gpt-6-astra` (highest intelligence,
  released Sep 3, 2026), `gpt-6-sol` and `gpt-6-luna` (released Sep 22), and
  `gpt-6.1-sol` (released Sep 29, the newer Sol; "See GPT-6.1 Sol for the
  newer Sol model"). The guide's model picker lists Astra, 6.1 Sol and Luna.
  Knowledge cutoffs: Astra and 6.1 Sol Apr 30, 2026; Sol Apr 20; Luna May 18.
- "GPT-6 also supports the existing API capabilities available with GPT-5.6,
  including computer use, Structured Outputs, streaming, Programmatic Tool
  Calling."
- Migration note: "replace `prompt_cache_retention` with
  `prompt_cache_options.ttl`".

**New harness-level features** [V] (Responses API only):

- **Async tool calling:** `async: true`. "GPT-6 can continue reasoning, call
  other tools, or answer independent parts of a request while your
  application runs a tool." Results return later by `call_id`.
- **Mid-turn steering:** send extra user instructions while the model works
  (over WebSocket).
- **Change effort mid-conversation:** a `configuration_update` input item
  raises or lowers reasoning effort without breaking the prompt cache.

**API constraints** [P]:

- "GPT-6 Astra and GPT-6.1 Sol support Chat Completions, but tool calling
  requires Responses. GPT-6 Sol and GPT-6 Luna support function calling in
  Chat Completions only with `reasoning_effort: "none"`."
- "GPT-6 Astra and GPT-6.1 Sol do not support `none`; use `low` instead."
  6.1 Sol also drops `minimal`.
- "When reasoning effort is not `none`, remove `temperature`, `top_p`, and
  `top_logprobs`." Also remove `logprobs` (Chat Completions) or
  `message.output_text.logprobs` from `include` (Responses).

**Suggested agent prompt text a regulated harness may need to override** [P].
These are not a built-in default. The guide offers them "as a starting point
across the GPT-6 model family":

- "Before asking the user clarifying questions, you should complete the work
  that is already authorized from context and necessary to make the proposed
  action concrete and reviewable."
- Introduced with "If you are implementing a multi-agent system in your
  harness, use the following prompt": "If at any point you can parallelize
  work by delegating tasks to another agent (no matter if you are the root or
  subagent), you should do so using collaboration tools if it could save time
  or improve quality."
- "Do not write tests for reversible, low-impact changes that mirror the
  implementation."

**Governance-relevant notes** [P]:

- "Fast mode is not available with EU data residency for GPT-6 Astra, GPT-6
  Sol, or GPT-6 Luna." The 6.1 Sol model page says the same separately.
  Ultrafast mode supports only US data residency and global processing.
- "As part of our strengthened safeguards for GPT-6 Astra, our systems
  asynchronously monitor for misalignment and trigger alerts when necessary."
  The changelog adds that this applies "in supported Responses API requests.
  Checks can trigger safety alerts or stop a conversation for review." A bank
  should know a vendor-side check can halt a session.

## 3. How this updates round 1's "where the labs disagree" file

`track2-vendor-disagreements.md` §3 (multi-agent) said OpenAI treats
multi-agent as an escalation you earn after single-agent failure. The GPT-6
guide's suggested prompt for harnesses that already run multiple agents tells
the model to delegate when parallel work "could save time or improve
quality." That is guidance for teams that have already chosen multi-agent,
not advice to choose it, so the shift is smaller than round 2 first said.
On how to use subagents once you have them, the two labs' guidance has moved
closer. On whether to start with them, the 2025 "practical guide" PDF that
round 1 quoted has not been replaced.

## 4. Google: Gemini 3.x guidance [P]

All quotes checked word for word against the raw ai.google.dev pages on
2026-09-30, except where marked. Quotes from blog.google and the DeepMind model
card came through a summarising fetch tool; spot-check them before a slide.

### 4.1 Which models exist

- **The current generation is Flash only.** Newest stable: `gemini-3.8-flash`
  (GA Sep 2, 2026). Earlier: 3.7 Flash (Aug 13), 3.6 Flash and 3.5 Flash-Lite
  (Jul 21), 3.5 Flash (May 19). The only Pro is `gemini-3.1-pro-preview`,
  still a preview (ai.google.dev/gemini-api/docs/models and /changelog).
- **Gemini 3.5 Pro has not shipped.** May 19: "rolling it out next month."
  Jul 21: "Gemini 3.5 Pro is currently testing with partners and we plan to
  make it broadly available as soon as it's ready." (blog.google)
- "For any new projects, use our latest models: 3.5 Flash-Lite or 3.8
  Flash." 2.5 models are limited to past users.
- 3.8 Flash: 1,048,576 input and 65,536 output tokens; computer use is
  "Preview". Google's own Antigravity agent and SDK use it by default.
- Google says 3.8 Flash "works harder. On complex tasks, it exhibits greater
  diligence ... executing extra reasoning steps, and calling tools
  iteratively" (blog.google). Expect more tool calls and tokens per task.

### 4.2 Thinking levels

- `thinking_level` replaces `thinking_budget`: "You cannot use both ... in the
  same request. Doing so will return a 400 error."
  (ai.google.dev/gemini-api/docs/gemini-3)
- 3.8 Flash has low, medium (default; "Recommended for complex code and
  agentic use cases") and high. "`minimal` thinking level is not supported
  for Gemini 3.8 Flash and will return an error."
- **The default differs by model**: medium for 3.5 to 3.8 Flash, minimal for
  3.5 Flash-Lite, high for 3.1 Pro preview and 3 Flash preview
  (docs/thinking, updated Sep 25). 3.5 Flash lowered it: "Default effort
  changed from `high` → `medium`". Pin the level in config so a model upgrade
  does not silently change it.
- Too many tool calls? "Higher thinking levels encourage the model to use more
  tools to explore and verify, so lowering the level can reduce tool calls."
  Then a system instruction such as "You have a limited action budget of <n>
  tool calls."

### 4.3 Temperature: remove it

- 3.8 migration checklist: "Strip `temperature`, `top_p`, and `top_k` from
  generation configs." `candidate_count` is "unsupported in Gemini 3 and
  later". (docs/latest-model)
- "For all Gemini 3 models, we strongly recommend keeping the temperature
  parameter at its default value of 1.0." Changing it "may lead to
  unexpected behavior, such as looping or degraded performance".
- **For bank teams that pin temperature to 0:** "If your existing code
  explicitly sets temperature (especially to low values for deterministic
  outputs), we recommend removing this parameter". Google's replacement: "To
  ensure determinism, we recommend defining a system instruction with
  explicit rules for your specific use case." OpenAI says the same for
  reasoning models (§2), so all three labs now agree.

### 4.4 Migrating old prompts

- "If you were previously using complex prompt engineering (like chain of
  thought) to force Gemini 2.5 to reason, try Gemini 3 with
  `thinking_level: "high"` and simplified prompts."
- "Be concise. Gemini 3.x responds best to direct, clear instructions.
  Verbose or complex prompt engineering techniques designed for older models
  may cause the model to over-analyze." Same thin-harness point as Anthropic
  and OpenAI.
- "Standardize multi-turn conversations on server-side
  `previous_interaction_id`. Remove prefilled model turns."
- Thought signatures (encrypted reasoning passed between turns): "pass the
  full, unmodified conversation history (including thought signatures) in
  `contents`." A harness that trims or rewrites history loses them; the
  checklist says this "may increase token usage".

### 4.5 Function calling

- "Keep active set to 10-20 tools maximum." "Validate function calls before
  executing." (docs/function-calling)
- Parallel and compositional (chained) calls are supported. Modes via
  `tool_choice`: `auto` (default), `any`, `none`, `validated` ("Model ensures
  function schema adherence").
- Asking for structured text right before a tool call can cause
  `Malformed_Function_Call`. Fix: "Instruct the model to put its pre-tool
  notes inside a dedicated `update()` function call instead of raw text".
- Every `FunctionResponse` needs `call_id` and `name` (the 3.5 page calls the
  field `id`).

### 4.6 Long context, caching, system instructions

- "Place your specific instructions or questions at the very *end* of the
  prompt." (docs/prompting-strategies)
- With several facts to find, "the model does not perform with the same
  accuracy" as with one (docs/long-context).
- "Implicit caching is enabled by default for all Gemini 2.5 and newer
  models"; minimum 4,096 tokens for 3.5 to 3.8 Flash. "Try putting large and
  common contents at the beginning of your prompt". Keep the system prompt
  and tool definitions as a fixed prefix.
- The agentic guidance lists "Risk Assessment: ... Explicitly distinguishes
  between low-risk exploratory actions (reads) and high-risk state changes
  (writes)" and "Ambiguity and permission handling".
- Stale example in the docs: a suggested system instruction "Your knowledge
  cutoff date is January 2025" was written for 3 Flash. Do not copy it.

### 4.7 Computer use

- Recommended model: 3.8 Flash. "As a Preview capability, Computer Use may
  contain errors and security vulnerabilities ... avoid using the Computer
  Use capability for tasks involving critical decisions, sensitive data, or
  actions where serious errors cannot be corrected." Run it "in a sandboxed
  VM or container". Screenshot prompt-injection detection is "opt-in".
