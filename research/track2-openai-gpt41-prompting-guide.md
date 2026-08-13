---
url: https://developers.openai.com/cookbook/examples/gpt4-1_prompting_guide
fetched: 2026-08-12
---

# OpenAI Cookbook — GPT-4.1 Prompting Guide (Apr 2025)

The canonical late-instruct-era document: a NON-reasoning model that must be told, verbatim, to persist, use tools, and plan. Perfect "before" exhibit for the generation shift.

## Literal instruction following (quotable)
> "GPT-4.1 is trained to follow instructions more closely and more literally than its predecessors, which tended to more liberally infer intent from user and system prompts."

Steering is cheap:
> "if model behavior is different from what you expect, a single sentence firmly and unequivocally clarifying your desired behavior is almost always sufficient to steer the model on course."

## The three agentic reminders (the era's signature scaffolding — quotable verbatim)
1. **Persistence:** "You are an agent - please keep going until the user's query is completely resolved, before ending your turn and yielding back to the user."
2. **Tool-calling:** "If you are not sure about file content or codebase structure pertaining to the user's request, use your tools to read files and gather the relevant information: do NOT guess or make up an answer."
3. **Planning (optional):** "You MUST plan extensively before each function call, and reflect extensively on the outcomes of the previous function calls."

These three instructions raised OpenAI's internal SWE-bench Verified score by ~20%.

## Induced chain-of-thought (because the model has none)
> "GPT-4.1 is not a reasoning model—meaning that it does not produce an internal chain of thought before answering."
Prompted step-by-step "thinking out loud" raised agentic pass rates by 4%.

## Long context & structure
- 1M context: put instructions at BOTH beginning and end of long context.
- Delimiters: markdown for prompt sections; for large document sets, "XML and pipe-delimited formats outperformed JSON significantly in testing."
- Conflicts: "GPT-4.1 tends to follow the one closer to the end of the prompt."
- Avoid over-relying on caps lock or reward language unless necessary.

## The empiricism line (quotable)
> "AI engineering is inherently an empirical discipline, and large language models are inherently nondeterministic; in addition to following this guide, we advise building informative evals and iterating often to ensure your prompt engineering changes are yielding benefits for your use case."
> — OpenAI, GPT-4.1 Prompting Guide
