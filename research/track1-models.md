---
url: https://docs.github.com/en/copilot/reference/ai-models/supported-models, https://docs.github.com/en/copilot/reference/copilot-billing/models-and-pricing, https://docs.github.com/en/copilot/concepts/models/auto-model-selection, https://docs.github.com/en/copilot/get-started/plans, https://docs.github.com/en/copilot/concepts/billing/billing-for-individuals, https://docs.github.com/en/copilot/reference/ai-models/model-comparison
fetched: 2026-08-12
---

# Models, model picker, AI credits (as of Aug 2026)

## HEADLINE: "Premium requests" are DEAD (legacy). Billing = AI credits.

- "As of June 1, 2026, GitHub replaced request-based billing with usage-based billing" — cost now depends on "the model and the number of tokens consumed". The whole premium-request/multiplier system is filed under "request-based billing (legacy)":
  https://docs.github.com/en/copilot/reference/copilot-billing/request-based-billing-legacy/what-changed-with-billing
- **1 AI credit = $0.01 USD** (https://docs.github.com/en/copilot/reference/copilot-billing/models-and-pricing)
- Annual Pro/Pro+ subscribers may stay on legacy premium-request billing or switch (prorated credits).
- "Code completions and next edit suggestions are not billed in AI credits. They remain unlimited for all paid Copilot plans."

## Plans (https://docs.github.com/en/copilot/get-started/plans)

| Plan | Price | AI credits/month (base + flex) |
|---|---|---|
| Copilot Free | — | no credits; 2,000 code completions |
| Copilot **Student** (new plan) | Free | unlimited completions |
| Copilot Pro | $10/mo | 1,000 + 500 flex = 1,500 |
| Copilot Pro+ | $39/mo | 3,900 + 3,100 flex = 7,000 |
| Copilot **Max** (NEW plan, not in 2025) | $100/mo | 10,000 + 10,000 flex = 20,000 |
| Copilot Business | $19/seat/mo | per-user allowance (see billing docs) |
| Copilot Enterprise | $39/seat/mo | per-user allowance (see billing docs) |

(Credit allowances from https://docs.github.com/en/copilot/concepts/billing/billing-for-individuals)

- Cloud agent: all paid plans incl. Student; NOT Copilot Free.
- Free/Student model access is "through auto model selection only" — no manual picker on free tiers.
- Credits consumed by: Copilot Chat, Copilot CLI, cloud agent, Spaces, **Spark**, third-party coding agents.

## Current model list (https://docs.github.com/en/copilot/reference/ai-models/supported-models, fetched 2026-08-12)

**OpenAI (GA):** GPT-5 mini, GPT-5.3-Codex, GPT-5.4, GPT-5.4 mini, GPT-5.4 nano, GPT-5.5, GPT-5.6 Luna, GPT-5.6 Sol, GPT-5.6 Terra
**Anthropic (GA):** Claude Fable 5, Claude Haiku 4.5, Claude Opus 4.5, Claude Opus 4.6, Claude Opus 4.7, Claude Opus 4.8, Claude Opus 4.8 (fast mode — Preview), Claude Opus 5, Claude Sonnet 4.5, Claude Sonnet 4.6, Claude Sonnet 5
**Google:** Gemini 3.1 Pro (public preview), Gemini 3.5 Flash (GA), Gemini 3.6 Flash (GA)
**Microsoft (GA, NEW first-party models):** MAI-Code-1-Flash, MAI-Code-1.1-Flash
**Others (GA):** Raptor mini (fine-tuned GPT-5 mini), Kimi K2.7 Code (Moonshot AI), Kimi K3 (Moonshot AI), Grok 4.5 (xAI)

Restrictions noted on the page: GPT-5.4 mini and Claude Haiku 4.5 unavailable in cloud agent; Raptor mini only in Copilot Chat.

### Extended capabilities (per supported-models page)

Models supporting **1 million-token context window** + configurable reasoning effort: Claude Sonnet 4.6, Claude Opus 4.6/4.7/4.8, Claude Opus 5, Claude Sonnet 5, GPT-5.3-Codex, GPT-5.4, GPT-5.5, GPT-5.6 variants, Kimi K3. (Claude Opus 4.8 fast mode: reasoning levels but no extended context.)

## Per-model token pricing (sample, per 1M tokens — models-and-pricing reference)

| Model | Input | Cached input | Output |
|---|---|---|---|
| GPT-5 mini | $0.25 | $0.025 | $2.00 |
| Claude Haiku 4.5 | $1.00 | $0.10 | $5.00 |
| Gemini 3.5 Flash | $1.50 | $0.15 | $9.00 |
| Claude Opus 5 | $5.00 | $0.50 | $25.00 |

(Full tables on the live page: https://docs.github.com/en/copilot/reference/copilot-billing/models-and-pricing)

## Auto model selection (https://docs.github.com/en/copilot/concepts/models/auto-model-selection)

- Verbatim: paid-plan users "qualify for a **10% discount on model costs** while using auto model selection in Copilot Chat, Copilot CLI, GitHub Copilot app, or Copilot cloud agent."
- Mechanism: "One system tracks real-time system health and availability, while the other evaluates task complexity. Putting these together, auto model selection routes the task to the optimal model."
- Free/Student plans: auto model selection is the ONLY access mode.
- Admins can manage which models auto-selection may use (docs nav: "Managing default models", "AI model access configuration").

## Model comparison guidance (https://docs.github.com/en/copilot/reference/ai-models/model-comparison)

Categories: **general-purpose** (GPT-5 mini "Reliable default", GPT-5.3-Codex "higher-quality code on complex engineering tasks", GPT-5.6 Terra, MAI-Code-1-Flash, Raptor mini, Kimi K2.7 Code), **fast** (GPT-5.6 Luna "Lightweight, cost-efficient", Claude Haiku 4.5, Gemini 3.5/3.6 Flash), **deep reasoning** (GPT-5.4/5.5/5.6 Sol, Claude Opus 4.7/4.8/5, Claude Sonnet 4.6, Gemini 3.1 Pro "Advanced reasoning across long contexts"), **visual/multimodal** (GPT-5 mini, Claude Sonnet 4.6, Gemini 3.1 Pro). This page does NOT publish per-model context-window numbers.

## Other model-related surfaces (docs nav; sources for deeper dives)

- **BYOK** ("Bring Your Own Key") — external-provider models in IDE, CLI (`use-byok-models`), and Copilot app; enterprise "Enabling custom models".
- "Utility models", "FedRAMP-compliant models", "Base and LTS models" concept pages exist (Models & Tools section of https://docs.github.com/en/copilot).
- Model hosting reference: https://docs.github.com/en/copilot/reference/ai-models/model-hosting
- Picker how-tos: "Chat model switching", "Inline suggestion model changing" (https://docs.github.com/en/copilot/how-tos/use-ai-models/change-the-chat-model).

## Contradictions vs 2024-2025 common knowledge

- No more 0x/0.33x/1x multiplier tables — token-based AI credits instead (legacy pages preserved for annual-plan holders).
- Two new plans: **Student** (free, unlimited completions) and **Max** ($100).
- Microsoft now ships its own first-party coding models (MAI-Code) inside Copilot, plus Moonshot (Kimi) and xAI (Grok) third-party models.
- 1M-token context windows are now a documented Copilot capability tier.
