---
url: https://platform.claude.com/docs/en/build-with-claude/compaction
url2: https://platform.claude.com/docs/en/build-with-claude/context-editing
url3: https://platform.claude.com/docs/en/agents-and-tools/tool-use/memory-tool
fetched: 2026-08-12
---

# Anthropic docs — Context management: compaction, context editing, memory tool

Three complementary mechanisms; all three are now *platform features*, i.e., context engineering moved from prompt-craft into API infrastructure.

## 1. Server-side compaction (beta `compact-2026-01-12`)
- "Compaction extends the effective context length for long-running conversations and tasks by automatically summarizing older context when approaching the context window limit."
- Server-side: "handles context management automatically, without client-side summarization code."
- Flow: hit trigger threshold (default 150k input tokens) → generate summary → emit a `compaction` block → "the API automatically drops all content blocks prior to the compaction block, continuing the conversation from the summary."
- "Server-side compaction is the recommended strategy for managing context in long-running conversations and agentic workflows."
- Custom `instructions` REPLACE the default summarization prompt entirely. Default prompt: "Write down anything that would be helpful, including the state, next steps, learnings etc."
- Billing: compaction is an extra sampling step; sum `usage.iterations`.

## 2. Context editing (`clear_tool_uses_20250919`, `clear_thinking_20251015`)
Quotable framing:
> "Beyond optimizing costs and staying within limits, this is about actively curating what Claude sees: context is a finite resource with diminishing returns, and irrelevant content degrades model focus."
> — Anthropic, Context editing docs

- Tool-result clearing: "the API automatically clears the oldest tool results in chronological order... replaces each cleared result with placeholder text so Claude knows it was removed." Options: trigger, keep-N, clear_at_least, exclude_tools, clear_tool_inputs.
- Thinking-block clearing: keep last N thinking turns or all; model-generation defaults shifted (Opus 4.5+/Sonnet 4.6+ keep all thinking by default; older models kept only last turn).
- Client keeps full history; only what Claude *sees* is edited.
- Positioning: "For most use cases, server-side compaction is the primary strategy... The strategies on this page are useful for specific scenarios where you need more fine-grained control."

## 3. Memory tool (`memory_20250818`, GA)
- "The memory tool lets Claude store and retrieve information across conversations in a directory of memory files... building up knowledge over time without keeping everything in the context window."
- "Memory supports just-in-time context retrieval. Rather than loading all relevant information up front, an agent records what it learns in memory files and reads them back on demand." (docs link this directly to the Effective context engineering post)
- Client-side: Claude requests file ops (view/create/str_replace/insert/delete/rename under `/memories`); your app executes them. Path-traversal protection is your job.
- The API auto-injects a memory system prompt, including: "IMPORTANT: ALWAYS VIEW YOUR MEMORY DIRECTORY BEFORE DOING ANYTHING ELSE." and "ASSUME INTERRUPTION: Your context window might be reset at any moment, so you risk losing any progress that is not recorded in your memory directory."
- Combined doctrine: "compaction keeps the active context small without client-side bookkeeping, and memory preserves the information that must survive summarization."
- Docs codify the **multisession pattern** (initializer session sets up progress log + feature checklist; later sessions read them; end-of-session update) — the productized version of the "Effective harnesses" engineering post.

## Slide relevance
2023: developers hand-rolled truncation and summarization in app code. 2026: summarization (compaction), pruning (context editing), and persistence (memory tool) are first-class vendor API features with model-aware defaults.
