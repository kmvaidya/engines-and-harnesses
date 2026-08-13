---
url: https://code.visualstudio.com/docs/agent-customization/prompt-files, https://docs.github.com/en/copilot/reference/customization-cheat-sheet
fetched: 2026-08-12
---

# Prompt files (`*.prompt.md`)

## Location

- Workspace default: **`.github/prompts/`** (configurable via `chat.promptFilesLocations`).
- User profile: VS Code profile user-data folder — available across all workspaces, synced via Settings Sync ("Prompts and Instructions").
- GitHub cheat sheet confirms repo path `.github/prompts/*.prompt.md` and notes **github.com has NO prompt-file support** (IDE feature).
  (Sources: https://code.visualstudio.com/docs/agent-customization/prompt-files ; https://docs.github.com/en/copilot/reference/customization-cheat-sheet)

## Frontmatter fields (ALL optional)

| Field | Purpose |
|---|---|
| `description` | short description |
| `name` | display name when typing `/` in chat (defaults to filename) |
| `argument-hint` | hint text shown in the chat input |
| `agent` | which agent runs it: `ask`, `agent`, `plan`, or a **custom agent name** |
| `model` | model to use (falls back to current picker selection) |
| `tools` | list of allowed tools; supports `<server-name>/*` wildcard for MCP servers |

**CHANGE vs 2025:** the old `mode:` field is now **`agent:`** (values were `ask`/`edit`/`agent`; now `ask`, `agent`, `plan`, or custom agent name — `edit` is gone from the documented values). Tool-priority rule (verbatim): "Tool availability determined by: prompt tools → agent tools → default tools priority" and "When you use `tools` in both a custom agent and a prompt file, the prompt file's tools take precedence."

## Invocation

- **Slash command** in chat: `/prompt-name`, with arguments: `/prompt-name argument=value`, e.g. `/create-react-form formName=MyForm`.
- Command Palette: **Chat: Run Prompt**.
- **Play button** in the prompt-file editor title bar.
- `/prompts` in chat opens the Configure Prompt Files menu.

## Variables

- `${input:variableName}` and `${input:variableName:placeholder}` — user input
- `${selection}` — current selection
- `#tool:<tool-name>` — tool reference in the body (e.g. `#tool:browser`)
- Markdown links with relative paths pull in workspace files.

## Verbatim examples (from VS Code docs)

```markdown
---
agent: 'agent'
model: GPT-4o
tools: ['search/codebase', 'vscode/askQuestions']
description: 'Generate a new React form component'
---
Your goal is to generate a new React form component based on
the templates in the Github repo contoso/react-templates.
```

```markdown
---
agent: 'ask'
model: Claude Sonnet 4
description: 'Perform a REST API security review'
---
Perform a REST API security review and provide a TODO list
of security issues to address.
```

## Presentation-worthy constraints

- "Agents on Agent Host don't use prompt files (convert to agent skills instead)" — prompt files only work with **local agents in the VS Code extension host**. There is a migration setting `chat.customizations.promptMigration.enabled` to **convert prompts to skills** — signals prompt files are being superseded by Agent Skills for hosted agents.
- `chat.promptFilesRecommendations` — surfaces prompts as recommended actions.
- Tools now use namespaced ids (`search/codebase`, `web/fetch`, `vscode/askQuestions`) — different from flat 2025 names (`codebase`, `fetch`).
- Docs are silent on prompt-file size limits.
