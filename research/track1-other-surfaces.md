---
url: https://docs.github.com/en/copilot, https://docs.github.com/en/copilot/concepts/agents/about-github-agentic-workflows, https://docs.github.com/en/copilot/how-tos/github-agentic-workflows/creating-github-agentic-workflows, https://docs.github.com/en/copilot/concepts/agents/cloud-agent/about-automations, https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot
fetched: 2026-08-12
---

# Other customization / AI-engineering surfaces (everything not in the other files)

## 1. GitHub Agentic Workflows (public preview) — markdown-defined AI automations

Sources: https://docs.github.com/en/copilot/concepts/agents/about-github-agentic-workflows, https://docs.github.com/en/copilot/how-tos/github-agentic-workflows/creating-github-agentic-workflows

- "AI-powered automations that run in your repositories on a schedule or in response to events" producing "ready-to-review outputs, such as issues, comments, and pull requests."
- Files live in **`.github/workflows/` as Markdown files with YAML frontmatter**, compiled to `.lock.yml` GitHub Actions files via the **`gh aw` CLI extension** (`gh extension install github/gh-aw`, `gh aw compile`).
- Frontmatter: `on` (Actions trigger syntax, plus natural-ish forms like `weekly on monday`), `permissions` (default `read-all`), **`engine`: `copilot`, `claude`, `codex`, or `gemini`** (multi-vendor!), `safe-outputs` (validated write ops: `create-issue`, `add-comment`, `create-pull-request`), `tools` (e.g. `github: toolsets: [issues]`), `network`.
- Security model: "Workflows have read-only repository permissions unless you explicitly grant more" and writes happen ONLY "through validated safe-outputs declared in the frontmatter."
- Verbatim complete example (docs):

```markdown
---
on: weekly on monday

permissions:
  issues: read
  copilot-requests: write

network: defaults

tools:
  github:
    toolsets: [issues]

safe-outputs:
  create-issue:

---

# Weekly issue activity report

Review issue activity from the last 7 days in this repository.

Create a GitHub issue that includes:

- Total issues opened and closed this week.
- The top recurring themes from issue titles and descriptions.
- A short list of notable issues that still need attention.
- Two or three actionable recommendations for maintainers.

Keep the report concise and action-oriented.
```

## 2. Copilot automations (agent scheduling UI)

Source: https://docs.github.com/en/copilot/concepts/agents/cloud-agent/about-automations, https://docs.github.com/en/copilot/how-tos/use-copilot-agents/cloud-agent/create-automations

- "Create and manage automations to run Copilot cloud agent on a schedule or in response to events." Triggers: hourly/daily/weekly schedule, or when an issue is created.
- Define: name + prompt + trigger(s); optionally model and allowed tools ("pushing changes, updating issue labels, or creating a pull request").
- Managed in the **Agents tab** of a repo. Plans: Pro, Pro+, Max, Business, Enterprise. **"Available in private and internal repositories only."**

## 3. Copilot CLI — full customization stack

Source: https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot

The CLI supports ALL of: custom instructions (repo + `~/.copilot/copilot-instructions.md`), `/settings`, hooks (`~/.copilot/hooks/*.json`), agent skills, MCP servers, custom agents, **BYOK external LLM models** ("Use a model from an external provider of your choice in Copilot by supplying your own API key"), and **plugins**. Subpage URLs listed under `/en/copilot/how-tos/copilot-cli/customize-copilot/*` (add-custom-instructions, use-hooks, add-skills, add-mcp-servers, create-custom-agents-for-cli, use-byok-models, plugins-finding-installing, plugins-creating, plugins-marketplace).

CLI-only features from docs nav (https://docs.github.com/en/copilot): autopilot (autonomous execution), **`/fleet`** parallel tasks, `/chronicle` session data, "rubber duck agent", LSP servers, tool search, remote control / VS Code connection, prompt scheduling, GitHub Actions integration (automate-with-actions), programmatic execution, ACP server reference, "CLI configuration directory reference".

## 4. Plugins (new distribution mechanism)

- Docs nav shows: "Plugins", "Enterprise plugin standards" concepts; CLI plugin finding/creating + **plugin marketplace creation**; SDK "Plugin directories". Plugins bundle skills/hooks/MCP (skills get namespaced like `/my-plugin:test-runner` per VS Code skills docs; plugin `hooks.json` is a documented hook source in the hooks reference).
- VS Code overview lists "Agent Plugins" at https://code.visualstudio.com/docs/agent-customization/agent-plugins.

## 5. Copilot SDK

Docs nav has a full **Copilot SDK** section (https://docs.github.com/en/copilot — "SDK Development"): agent loop processing, cloud sessions, custom agents + sub-agent orchestration, fleet mode, hooks (pre/post tool use, session lifecycle, user-prompt-submitted, error handling), image input, MCP servers, session persistence/resume, custom skills, steering and queueing, streaming session events, BYOK/Azure managed identity, multi-tenancy, OpenTelemetry instrumentation, Microsoft Agent Framework integration. Copilot's agent runtime is now programmable like Claude's Agent SDK.

## 6. GitHub Copilot app (desktop) + third-party agents

- **GitHub Copilot app** — a desktop app with agent sessions, canvas extensions, automations, BYOK, deep links, repository configuration reference, slash-commands reference, built-in skills reference (docs nav).
- **Third-party agents / agent apps:** docs list "OpenAI Codex" and "Anthropic Claude" as agents usable on the GitHub platform ("Additional Agents" concepts; agentic workflows `engine:` field accepts claude/codex/gemini). GitHub is now multi-vendor at the agent level, not just the model level.

## 7. Sandboxing

- "Cloud and local sandboxes" concept + how-tos "Local sandboxing setup", "Local sandbox settings" (docs nav) — local agent execution sandboxing on the GitHub side.
- VS Code: MCP server sandboxing (`sandboxEnabled`, filesystem/network allowlists) — see track1-mcp.md.

## 8. Enterprise/org governance surface (docs nav)

- **`.github-private` repository** for org/enterprise-shared custom agents ("Creating `.github-private` repository").
- "Enterprise-managed settings" reference, "Policy support by surface" reference, "Blocking agentic features", "Monitoring agentic activity", agent session filters, audit-log events for agents.
- MCP: allowlist configuration, registry configuration, restricting registry access, private registry enforcement (see track1-mcp.md).
- Copilot policies: "AI credits paid usage", "Allow members without a Copilot license to use Copilot code review" (see track1-code-review.md).
- Content exclusion: how-tos "Excluding content from Copilot" / "Reviewing exclusion changes" — excluded content also filtered from semantic indexes (see track1-context.md).
- "Network settings" (proxy/allowlist) personal + enterprise.

## 9. Cloud agent trust UX

Docs nav: "Rationale, confidence, and approvals management" — cloud agent sessions expose rationale/confidence and approval gates (how-to under Cloud Agent Usage). Also "Research, plan, iterate workflow" and "Agent session management".

## 10. GitHub Spark

Concept + tutorials in docs nav (first Spark app, deploying from CLI, "Managing Spark" for enterprises). Spark consumes AI credits (listed among credit-consuming features in billing docs).

## 11. Agent finder / Agentic Resource Discovery

MCP concept page: "Agent finder supplements this by discovering capabilities at runtime using the Agentic Resource Discovery specification" (https://docs.github.com/en/copilot/concepts/context/mcp) — a new discovery spec beyond static MCP registry listings.

## 12. VS Code extras

- **Agent Host**: user-level harness-agnostic folders `~/.copilot` and `~/.claude`; Agent Host agents don't use prompt files (skills instead); native `.mcp.json` reading. (https://code.visualstudio.com/docs/agent-customization/overview, .../mcp-servers, .../prompt-files)
- **Chat Customizations Evaluations extension**: "analyzes customization files for logical contradictions and ambiguous wording", integrates the **Waza** evaluation framework for skills testing, `/analyze-prompt` slash command. (https://code.visualstudio.com/docs/agent-customization/overview)
- Custom language-model config page: https://code.visualstudio.com/docs/agent-customization/language-models (BYOK in VS Code).

## Explicitly absent / silent

- Docs are silent on any Copilot equivalent of "output styles".
- No "Copilot Extensions"/GitHub-App-based chat extensions section surfaced in the current docs nav fetch (the 2024-2025 "Copilot Extensions" program does not appear in the customization docs anymore); docs are silent on its status on the pages fetched.
- Docs are silent on hard per-file size limits for instruction/prompt/agent files (only skills have documented limits: name ≤64 chars, description ≤1024 chars).
