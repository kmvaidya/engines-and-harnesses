---
url: https://docs.github.com/en/copilot/concepts/agents/coding-agent/about-coding-agent, https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/customize-the-agent-environment, https://docs.github.com/en/copilot/how-tos/use-copilot-agents/cloud-agent/customize-the-agent-firewall
fetched: 2026-08-12
---

# Copilot cloud agent (the artist formerly known as "coding agent")

## NAME CHANGE (slide-worthy)

The feature is now officially **"GitHub Copilot cloud agent"** everywhere in the docs (URLs still contain `coding-agent` in places, and enterprise-cloud pages still say "Copilot coding agent" in old titles). 2024-2025 decks saying "Copilot coding agent" are out of date.
(Source: https://docs.github.com/en/copilot/concepts/agents/coding-agent/about-coding-agent)

## What it is / how work is assigned

An autonomous agent that works in the cloud and raises PRs. Task assignment methods (from the About page):
- **Assign Copilot to a GitHub Issue** (as assignee)
- **Copilot Chat on github.com**
- **`@copilot` mentions in PR comments**
- **VS Code** (delegate from the IDE)
- **Third-party integrations: Azure Boards, JIRA, Linear, Slack, Teams** (+ Raycast per docs nav)
- **Copilot automations** — scheduled/automated kickoff (new surface, see track1-other-surfaces.md)
- Also per docs nav: from GitHub CLI, via API, and via MCP ("Cloud agent via MCP").

## Environment

Verbatim: an "ephemeral development environment, powered by GitHub Actions, where it can explore your code, make changes, execute automated tests and linters".

- **Hard limit: "Maximum execution time of 59 minutes. This is a hard limit that cannot be extended or bypassed."**
- One repository per session; one branch + one PR per task; GitHub-hosted repos only; incompatible with certain branch-protection rules.
- Cost: covered by **GitHub Actions minutes + AI credits** (see track1-models.md — "premium requests" are legacy; billing is AI credits now).
- Plans: "Available for all paid Copilot plans" (Business/Enterprise need admin enablement).
- Model: user "may be able to select the model" depending on how the task is initiated ("Changing AI models" how-to exists for cloud agent).

## `copilot-setup-steps.yml`

Path: **`.github/workflows/copilot-setup-steps.yml`** — must exist on the **default branch**. It "looks like a normal GitHub Actions workflow file, but must contain a single `copilot-setup-steps` job" (exact job name required or it's not recognized).

Only these job keys are honored: **`steps`, `permissions`, `runs-on`, `services`, `snapshot`, `timeout-minutes` (max 59)** — anything else is ignored. If a setup step fails, remaining steps are skipped.

Verbatim starter YAML (from docs):

```yaml
name: "Copilot Setup Steps"

on:
  workflow_dispatch:
  push:
    paths:
      - .github/workflows/copilot-setup-steps.yml
  pull_request:
    paths:
      - .github/workflows/copilot-setup-steps.yml

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    permissions:
      contents: read
    steps:
      # ...
```

- **Larger runners:** `runs-on: ubuntu-4-core` style.
- **Self-hosted runners:** supported (NEW vs 2025) — Ubuntu x64 and Windows 64-bit only; "We recommend that you only use Copilot cloud agent with ephemeral, single-use runners"; must disable the integrated firewall; `runs-on: arc-scale-set-name`; proxy envs `https_proxy`/`http_proxy`/`no_proxy`, `ssl_cert_file`, `node_extra_ca_certs`.
- **Windows environments** possible via self-hosted or larger runners w/ Azure private networking (firewall incompatible).
- Git LFS: add checkout step with `lfs: true`.
- Secrets/variables for the agent are set in repo "Agents" variables/secrets (docs nav: "Secrets and variables setup").
(Source: https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/customize-the-agent-environment)

## Firewall

(Source: https://docs.github.com/en/copilot/how-tos/use-copilot-agents/cloud-agent/customize-the-agent-firewall)

- On by default with a **recommended allowlist**: OS package repos, container registries, language package registries, certificate authorities, Playwright browser hosts. Full list: https://docs.github.com/en/copilot/reference/copilot-allowlist-reference
- Configured in the **"Internet access" tab** of repo/org settings (UI-based; the 2025-era `COPILOT_AGENT_FIREWALL_ALLOW_LIST` env-var method is NOT mentioned on the current page — docs are silent on env-var configuration).
- Custom allowlist entries: **domain** form (`packages.contoso.corp` — includes subdomains) or **URL** form (`https://packages.contoso.corp/project-1/` — scheme+host+path-prefix scoped).
- Disabling: org can set "Enable firewall" → Disabled; warning: "will allow Copilot to connect to any host, increasing risks of exfiltration."
- Blocked request behavior (verbatim): "a warning is added to the pull request body (for new pull requests) or to a comment (for existing pull requests). The warning shows the blocked address and the command that tried to make the request."
- **Scope (verbatim): the firewall "only applies to processes started by the agent via its Bash tool. It does not apply to Model Context Protocol (MCP) servers or processes started in configured Copilot setup steps."** Not compatible with self-hosted runners.

## Env vars inside the agent sandbox (from hooks reference)

`GITHUB_COPILOT_API_TOKEN`, `GITHUB_COPILOT_GIT_TOKEN`, `COPILOT_AGENT_PROMPT` are set; **`GITHUB_TOKEN` is NOT set**. Working dir `/workspace` (cloned repo). (https://docs.github.com/en/copilot/reference/hooks-reference)

## Customization surface the cloud agent reads

- `.github/copilot-instructions.md`, `.github/instructions/*.instructions.md` (with `excludeAgent: "cloud-agent"` opt-out), AGENTS.md/CLAUDE.md/GEMINI.md, org instructions
- `.github/hooks/*.json` hooks
- `.github/skills/**/SKILL.md` agent skills
- Repo-level MCP config (GitHub MCP server + Playwright MCP server enabled by default)
- Copilot Memory (see track1-memory-spaces.md)
- Custom agents from `.github/agents/*.md` (see track1-custom-agents.md)

## New governance features (docs nav; see track1-other-surfaces.md)

"Rationale, confidence, and approvals management", agent session monitoring/filters, audit-log events for agents, "Blocking agentic features" (enterprise), cloud/local sandboxes.
