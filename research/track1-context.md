---
url: https://code.visualstudio.com/docs/agents/reference/workspace-context, https://docs.github.com/en/copilot/concepts/indexing-repositories-for-copilot-chat, https://docs.github.com/en/copilot/reference/ai-models/supported-models
fetched: 2026-08-12
---

# Context window handling & workspace context

## VS Code workspace context (https://code.visualstudio.com/docs/agents/reference/workspace-context)

NOTE: page moved — old `/docs/copilot/reference/workspace-context` is now **`/docs/agents/reference/workspace-context`** ("How Copilot understands your workspace").

- **`@workspace` is no longer the headline** — the current page is written around **`#codebase`** and automatic tool use. Verbatim: "You don't need to add `#codebase` to your prompt." Agents invoke semantic search automatically when they need project context. (`@workspace` isn't mentioned on the current reference page at all — a change from 2024-2025 docs where @workspace was central.)
- **Semantic search**: finds code "by meaning rather than exact keywords" via embeddings; index maintained automatically; "parts of the index might be stored on your machine and parts might come from remote sources, but you don't need to manage this distinction."
- **Remote index**:
  - GitHub repos: index built/maintained by GitHub; "This index only needs to be built once per repository, which means it is often instantly available." Works for GitHub.com and GHE Cloud, **not** Enterprise Server.
  - **Azure DevOps repos: remote index too** (new vs 2025) — requires Microsoft account sign-in.
  - Anything else: local index; "The initial build can take a few minutes, after which the index is kept up to date in the background." Local indexing "currently enabled for personal accounts; off by default for organizations/enterprises."
- Commands: **"Build Codebase semantic index"** (Command Palette); status in "the Copilot status dashboard in the VS Code Status Bar."
- What agents can draw on: all indexable files except `.gitignore`'d; directory structure + file names; code symbols/definitions; currently selected or visible editor text; conversation history and prior tool results.
- **Gotcha (verbatim):** "`.gitignore` is bypassed if you have a file open or have text selected within an ignored file."
- Trimming noise: `.gitignore`, `files.exclude`, `search.exclude` — these "improve search relevance, speed up searches over large workspaces, and reduce the tokens consumed by search results."
- Scale claim: works "from those with five files to those with 500,000 files". **Docs are silent on hard token limits / context window sizes in this reference.**

## Repository indexing on github.com (https://docs.github.com/en/copilot/concepts/indexing-repositories-for-copilot-chat)

- Semantic code search index used by: Copilot Chat (GitHub + VS Code) and **Copilot cloud agent**.
- Automatic: "When you start a conversation with Copilot Chat that has a repository context, the repository is automatically indexed." Initial index ≤ ~60 s for large repos; updates "within seconds of you starting a new conversation."
- "There is no limit to how many repositories you can index." (2025 docs had per-account index limits — gone.)
- "Copilot will not use your indexed repository for model training."
- Content exclusion filters indexed data for org/enterprise users before it reaches Chat.

## Context window sizes per model

- The supported-models reference documents an extended-capability tier: models supporting a **1 million token context window** and configurable reasoning effort (Claude Sonnet 4.6+/Opus 4.6+/Opus 5/Sonnet 5, GPT-5.3-Codex/5.4/5.5/5.6 family, Kimi K3). (https://docs.github.com/en/copilot/reference/ai-models/supported-models)
- Beyond that tier flag, **docs are silent on exact per-model context-window token counts** on the comparison/reference pages fetched.

## Chat context controls (docs nav pointers)

- `#file`, `#codebase`, MCP resources via Add Context; MCP prompts via `/<server>.<prompt>` (VS Code MCP page).
- GitHub docs how-to "Optimizing Chat context" and concept "Context management" (CLI) exist in the nav: https://docs.github.com/en/copilot (Developer workflows / CLI concepts).
- Content exclusion: "Excluding content from Copilot" how-to (see track1-other-surfaces.md).
- Copilot Spaces are the curated-context mechanism on github.com and reach IDEs via the GitHub MCP server (see track1-memory-spaces.md).
- CLI has explicit **context management** (`/context`?) and **compaction** — the hooks reference documents a `preCompact` event, proving automatic context compaction exists in CLI/cloud agent (https://docs.github.com/en/copilot/reference/hooks-reference).
