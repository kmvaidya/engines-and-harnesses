---
url: https://docs.github.com/en/copilot/concepts/agents/about-agent-skills, https://code.visualstudio.com/docs/agent-customization/agent-skills, https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/add-skills
fetched: 2026-08-12
---

# Agent Skills — YES, Copilot supports them (open Agent Skills standard)

Definition (GitHub docs, verbatim): agent skills are "folders of instructions, scripts, and resources that Copilot can load when relevant to improve its performance in specialized tasks." Skills "adhere to the Agent Skills specification, which is an open standard used across multiple AI systems" (agentskills.io — the Anthropic-originated standard).
(Source: https://docs.github.com/en/copilot/concepts/agents/about-agent-skills)

## Supported surfaces (GitHub concepts page)

- Copilot **cloud agent**
- Copilot **code review**
- GitHub Copilot **CLI**
- GitHub Copilot **app** (desktop)
- **Agent mode in VS Code and JetBrains IDEs**

## Locations

Project (repo) skills — three supported directories:
- `.github/skills/<skill-name>/SKILL.md`
- `.claude/skills/`
- `.agents/skills/`

Personal skills:
- `~/.copilot/skills/`
- `~/.agents/skills/`
- (VS Code also lists `~/.claude/skills/`)

VS Code: extra locations via `chat.agentSkillsLocations`.
(Sources: GitHub concepts page + https://code.visualstudio.com/docs/agent-customization/agent-skills)

## SKILL.md format

Required frontmatter:
- `name` — "A unique identifier for the skill. Only lowercase letters, numbers, and hyphens are allowed" — **max 64 chars**; invalid characters "cause the skill to silently fail to load"
- `description` — what it does and when to use it — **max 1024 chars**

Optional (VS Code): `argument-hint`, `user-invocable` (default true), `disable-model-invocation` (default false), `context: fork` (experimental — run skill in a dedicated subagent; setting `github.copilot.chat.skillTool.enabled`).

Verbatim example (VS Code docs):

```
---
name: webapp-testing
description: Guide for testing web applications using Playwright.
Use this when asked to create or run browser-based tests.
---

# Web Application Testing with Playwright

This skill helps you create and run browser-based tests...
```

## Progressive disclosure (three levels, VS Code docs)

1. **Discovery** — only name + description read from frontmatter
2. **Instructions** — full SKILL.md body loaded when the skill matches or is invoked
3. **Resources** — referenced files loaded "only when it references them"

"You can install many skills without consuming context."

## Invocation

- Model-invoked automatically when relevant.
- Explicit: slash — CLI docs example: prompt `Use the /frontend-design skill to create a responsive navigation bar in React.` (https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-skills)
- Plugin-distributed skills are namespaced: `/my-plugin:test-runner`.
- **`gh skill`** GitHub CLI command exists for discovering and installing skills from repositories (GitHub concepts page).
- Skill sources to browse: `anthropics/skills` repo and `github/awesome-copilot`.

## Relationship to prompt files

VS Code is nudging users from prompt files toward skills: "Agents on Agent Host don't use prompt files (convert to agent skills instead)" and setting `chat.customizations.promptMigration.enabled` converts prompts to skills. (https://code.visualstudio.com/docs/agent-customization/prompt-files)

## Contradiction vs 2024-2025 common knowledge

- "Skills" in 2024 Copilot docs meant Copilot Extensions/chat skills (API plugins). 2026 "Agent Skills" are the Anthropic-style SKILL.md folders — a completely different feature with the same word.
- Copilot now natively reads `.claude/skills/` — Claude Code skill folders work in Copilot unchanged.
- Code review also uses skills (per concepts page support list) — not just chat/agents.
