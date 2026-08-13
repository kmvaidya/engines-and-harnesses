---
url: https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions, https://code.visualstudio.com/docs/agent-customization/custom-instructions, https://docs.github.com/en/copilot/reference/custom-instructions-support
fetched: 2026-08-12
---

# AGENTS.md support in GitHub Copilot / VS Code

## Yes — fully supported, with nesting

GitHub docs (add-repository-instructions page) say, for "Agent instructions":

- **`AGENTS.md` files can live ANYWHERE in the repo**; "nearest in directory tree takes precedence."
- Alternative: a **single `CLAUDE.md` or `GEMINI.md` in the repository root** is also honored as agent instructions.
  (Source: https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions)

## Which surfaces honor AGENTS.md (from the support matrix)

Source: https://docs.github.com/en/copilot/reference/custom-instructions-support

- **Copilot cloud agent** (github.com, and when launched from VS Code/JetBrains/Eclipse/Xcode): AGENTS.md + CLAUDE.md + GEMINI.md.
- **Copilot code review** (github.com): **AGENTS.md only** (not CLAUDE.md/GEMINI.md).
- **VS Code Copilot Chat**: AGENTS.md (and CLAUDE.md via separate setting).
- **Copilot CLI**: agent instructions supported.
- **github.com Copilot Chat (ask box)**: does NOT list AGENTS.md — chat on the website uses personal/repo-wide/org instructions only.

## VS Code specifics

Source: https://code.visualstudio.com/docs/agent-customization/custom-instructions

- `AGENTS.md` is read from workspace root; **subfolder (nested) AGENTS.md is experimental**, gated by setting **`chat.useNestedAgentsMdFiles`** — "The agent decides which to use based on edited files."
- Root AGENTS.md toggle: **`chat.useAgentsMdFile`**.
- `CLAUDE.md` support (toggle `chat.useClaudeMdFile`): searched in workspace root, `.claude/CLAUDE.md`, and `~/.claude/CLAUDE.md`.

## Precedence / interaction with copilot-instructions.md

- Per https://docs.github.com/en/copilot/concepts/prompting/response-customization the combined priority order is:
  personal → path-specific instructions → repository-wide (`.github/copilot-instructions.md`) → **agent instructions (AGENTS.md/CLAUDE.md/GEMINI.md)** → organization.
- All applicable sets are SENT TOGETHER ("All sets of relevant instructions are provided to Copilot"); precedence is a weighting, and docs advise avoiding conflicts.
- So AGENTS.md does NOT replace copilot-instructions.md; both are injected. copilot-instructions.md ranks higher in the documented priority list.

## Nested-precedence caveat (be careful on slides)

The official line is only "nearest in directory tree takes precedence" (GitHub) and "the agent decides which to use based on edited files" (VS Code). The docs do NOT fully specify the merge order/conflict algorithm for multiple ancestor AGENTS.md files — community issues (e.g. github/copilot-cli#3051, microsoft/vscode#271489) track gaps between surfaces. Docs are silent on the exact combination algorithm.

## Contradiction vs 2024-2025 common knowledge

- In mid-2025 AGENTS.md support was new/limited (coding agent only, single root file). Now: nested files, CLAUDE.md/GEMINI.md as documented alternatives in GitHub's own docs, and code review reads AGENTS.md too.
- VS Code treats CLAUDE.md (a Claude Code convention) as a first-class Copilot instruction source — cross-tool convergence.
