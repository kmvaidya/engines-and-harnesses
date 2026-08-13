---
url: https://code.visualstudio.com/docs/agent-customization/custom-agents, https://docs.github.com/en/copilot/reference/customization-cheat-sheet
fetched: 2026-08-12
---

# Custom agents (formerly "custom chat modes") — `.agent.md`

## The rename (confirmed in docs)

VS Code docs state verbatim: **"Custom agents were previously known as custom chat modes. The functionality remains the same, but the terminology has been updated."** Existing `.chatmode.md` files should be **renamed to `.agent.md`** and moved to the agents folder.
(Source: https://code.visualstudio.com/docs/agent-customization/custom-agents)

## Locations

- Workspace: **`.github/agents/`** (also `.claude/agents/` for Claude-format agents)
- User: **`~/.copilot/agents/`**
- Custom paths: `chat.agentFilesLocations` setting
- GitHub repo-hosted custom (cloud) agents: `.github/agents/AGENT-NAME.md`; org/enterprise-shared agents live in **`.github-private`** repos (per https://docs.github.com/en/copilot/reference/customization-cheat-sheet)

## Frontmatter fields (VS Code)

| Field | Type | Purpose |
|---|---|---|
| `name` | string | agent id; defaults to filename |
| `description` | string | placeholder text in chat input |
| `argument-hint` | string | user guidance |
| `tools` | array | allowed tools, e.g. `['search', 'web/fetch', 'read/file']`; `['<server-name>/*']` = all tools of an MCP server |
| `agents` | array | subagents this agent may invoke: `['Researcher', 'Implementer']`, `['*']` all, `[]` none |
| `model` | string OR **array** | model(s); an array is tried in priority order (fallback list) |
| `user-invocable` | boolean | show in dropdown (default true) |
| `disable-model-invocation` | boolean | prevent use as a subagent (default false) |
| `target` | string | `vscode` or `github-copilot` — same file can target the IDE or the cloud agent |
| `mcp-servers` | array | MCP server configs (for `github-copilot` target) |
| `handoffs` | array | workflow transitions between agents |
| `hooks` | object | agent-scoped hooks (Preview) |

## Handoffs (agent → agent workflow buttons)

"Each handoff specifies the target agent, the button label, and an optional prompt to send."

```yaml
handoffs:
  - label: Display text
    agent: target_agent_name
    prompt: Prompt text to send
    send: false  # Optional; auto-submit if true
    model: Model Name (vendor)
```

## Verbatim examples

Planning agent with model fallback + handoff:

```yaml
---
description: Generate an implementation plan for new features
name: Planner
tools: ['web/fetch', 'search/codebase', 'search/usages']
model: ['Claude Opus 4.5', 'GPT-5.2']
handoffs:
  - label: Implement Plan
    agent: agent
    prompt: Implement the plan outlined above.
    send: false
---
# Planning instructions
You are in planning mode. Generate implementation plans without making code edits.
```

Orchestrator with subagents:

```yaml
---
name: Feature Builder
description: Build features by researching first, then implementing
tools: ['agent']
agents: ['Researcher', 'Implementer']
---
You are a feature builder. For each task:
1. Use the Researcher agent to gather context
2. Use the Implementer agent to make code changes
```

Agent-scoped hooks (Preview):

```yaml
---
name: "Strict Formatter"
description: "Agent that auto-formats code after every edit"
hooks:
  PostToolUse:
    - type: command
      command: "./scripts/format-changed-files.sh"
---
You are a code editing agent. Files are automatically formatted after changes.
```

## Creating / invoking

- Command Palette: **Chat: New Custom Agent**
- `/agents` in chat input → agents list
- **`/create-agent`** in Agent mode: AI generates the agent file for you
- Subagent nesting: `chat.subagents.allowInvocationsFromSubagents`
- Org-level agents in VS Code: `github.copilot.chat.organizationCustomAgents.enabled`

## Contradictions vs 2024-2025 common knowledge

- `.chatmode.md` is legacy; the whole feature is now "custom agents" (`.agent.md`).
- Custom agents are no longer IDE-only: with `target: github-copilot` the same file defines a **cloud agent persona** usable on github.com; orgs/enterprises distribute agents via `.github-private` repos.
- Subagent orchestration (`agents:` list) and handoff buttons did not exist in the 2025 chat-modes feature.
- Models can be a fallback ARRAY, not just one string.

## GitHub side ("custom cloud agents") — reference page details

Source: https://docs.github.com/en/copilot/reference/custom-agents-configuration ("Custom agents configuration")

- Frontmatter properties (GitHub reference): `name` (optional display name), `description` (**required**), `target` (`vscode` | `github-copilot`; **defaults to both**), `tools` (defaults to ALL if unset), `model` (inherits default if unset), `disable-model-invocation` ("Disables Copilot cloud agent from automatically using this custom agent"), `user-invocable` (default true), `infer` (**retired** — use `disable-model-invocation`), `mcp-servers` (extra MCP servers/tools for this agent), `metadata` (key-value annotations).
- **Tool aliases** (case-insensitive): `execute`, `read`, `edit`, `search`, `agent`, `web`, `todo` (compat alternatives e.g. `shell`/`bash`/`powershell` for `execute`).
- Out-of-box MCP servers available to custom agents: **github** (read-only tools scoped to source repo) and **playwright** (browser automation, localhost-restricted, repo-scoped token).
- Minimal example (verbatim):

```
---
name: test-specialist
description: Focuses on test coverage, quality, and testing best practices
---

You are a testing specialist focused on improving code quality through comprehensive testing...
```

- Invocation: github.com (automatic or manual selection based on task), IDEs (manual selection), Copilot CLI. Versioning "uses Git commit SHAs".
- Related how-tos in the docs nav: "Custom cloud agent creation", "Preparing for custom agents" (org/enterprise via `.github-private` repo), "Custom agent testing and release", "Custom agents in IDE". See track1-coding-agent.md and track1-other-surfaces.md.
(Source: https://docs.github.com/en/copilot — navigation, fetched 2026-08-12)
