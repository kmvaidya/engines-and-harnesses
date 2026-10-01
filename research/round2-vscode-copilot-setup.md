---
url: https://code.visualstudio.com/docs/agents/reference/ai-features-cheat-sheet, https://code.visualstudio.com/docs/agent-customization/custom-instructions, https://code.visualstudio.com/updates/v1_109, https://code.visualstudio.com/updates/v1_110, https://code.visualstudio.com/updates/v1_126, https://code.visualstudio.com/docs/agents/guides/customize-copilot-guide, https://code.visualstudio.com/docs/agents/local-agents, https://code.visualstudio.com/docs/agents/concepts/agents, https://code.visualstudio.com/docs/agents/run/approvals, https://code.visualstudio.com/docs/agents/reference/ai-settings, https://code.visualstudio.com/docs/agents/run/review-code-edits, https://code.visualstudio.com/docs/agent-customization/agent-skills, https://code.visualstudio.com/docs/agents/agent-troubleshooting/troubleshooting, https://code.visualstudio.com/docs/agents/agent-troubleshooting/chat-debug-view, https://code.visualstudio.com/docs/enterprise/ai-settings, https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-command-reference, https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-config-dir-reference, https://docs.github.com/en/copilot/concepts/agents/copilot-in-jetbrains, https://docs.github.com/en/copilot/how-tos/copilot-in-your-ide/customize-copilot/configure-custom-instructions/add-repository-instructions-in-your-ide, https://github.blog/changelog/2026-03-11-major-agentic-capabilities-improvements-in-github-copilot-for-jetbrains-ides/, https://github.blog/changelog/2026-09-22-new-features-and-improvements-in-copilot-for-jetbrains/
fetched: 2026-10-01
---

# VS Code and JetBrains Copilot setup facts (for the Build Your Own Harness deck)

Round 2 file. Every item read from the live page on 2026-09-30 or 2026-10-01
(VS Code docs dated 9/30/2026, VS Code 1.139). Tag: **[P]** primary source.
Gathered by one research agent; not adversarially checked.

## Session targets [P]

- VS Code docs moved from `/docs/copilot/...` to `/docs/agent-customization/...`
  and `/docs/agents/...` (old URLs redirect).
- The **Session Target** control picks the harness: Local (extension host),
  Copilot (Agent Host, same runtime as Copilot CLI), Claude, Codex, plus Cloud.
- Local "will be removed in a future release" (settings reference). Many
  settings below are documented for Local only.

## /init [P]

- VS Code: "To generate project-wide instructions, type `/init`" (Local
  sessions). 1.109 notes: it discovers existing conventions files and
  "generates comprehensive workspace instructions". Output file not named.
- VS Code Copilot/Claude/Codex targets: **Chat: Open Customizations** →
  Overview prompt, e.g. "Analyze this codebase and create or update
  .github/copilot-instructions.md…".
- Copilot CLI: `copilot init` or `/init` "writes or updates a
  `.github/copilot-instructions.md` file".
- JetBrains: "Generate Agent Instructions" action creates `AGENTS.md`
  (changelog 2026-03-11); a `/init` tip exists (1.18.0) but output is undocumented.

## Agents and permission levels [P]

- Local agents: Ask (no changes), Plan ("uses read-only tools"), Agent (edits
  files, runs commands).
- Edit mode deprecated in 1.110, removed in 1.126. Settings reference and the
  GitHub feature matrix still list it (stale).
- Permissions dropdown: Manual (default), Assisted (experimental, LLM judge),
  Allow all. `chat.permissions.default` = `default` | `autoApprove` | `autopilot`.
  Autopilot auto-approves all tools. "Worktree sessions always use Allow all."
- Approval prompt: "approve a single use or grant approval for the session,
  workspace, or all future invocations."

## Approval settings [P]

- `chat.tools.global.autoApprove` (default false): "disables critical security
  protections". Per session: `/yolo`, `/disableYolo`.
- `chat.tools.terminal.autoApprove`: `true` auto-approves, `false` requires
  approval, `/regex/` allowed. Default already sets rm, rmdir, del, kill, curl,
  wget, eval, chmod, chown, Remove-Item to false. "A `false` rule requires
  approval. It does not block the command" (block with a PreToolUse hook).
- `chat.tools.edits.autoApprove`: glob map, default `{}`; docs example
  `"**/*": true, "**/.vscode/*.json": false, "**/.env": false`. System folders,
  dotfiles and files outside the workspace need confirmation by default (1.104).
- No dedicated VS Code permissions file a team can commit. Copilot CLI's
  `.github/copilot/settings.json` accepts only `deniedUrls`, `disabledSkills`,
  `disabledMcpServers` and `hooks` at repo level; `permissions.*` rules are
  managed/MDM only.

## Instructions and skills [P]

- Copilot target reads `.github/copilot-instructions.md` or `AGENTS.md`; Local
  also `CLAUDE.md`. "Applicable instruction sources are additive. Do not depend
  on a file order or precedence rule to resolve conflicts."
- Guidance: "Keep your instructions short and self-contained", "Include the
  reasoning behind rules", "Focus on non-obvious rules". No length limit given.
- Skills: project `.github/skills/`, `.claude/skills/`, `.agents/skills/`;
  personal `~/.copilot/skills/`, `~/.claude/skills/`, `~/.agents/skills/`
  (GitHub docs omit `~/.claude/skills`). `name` must match the folder,
  lowercase-hyphen, ≤64 chars, or the skill silently fails to load.
  Invoked by description match or `/skill-name`. `/create-skill` generates one.

## Seeing what loaded [P]

- References list under a response; **Chat: Open Customizations** (discovery,
  not use); Chat view menu → **Diagnostics**; **Developer: Show Chat Debug
  View**; Agent Debug Logs (preview); `/troubleshoot …`.

## JetBrains [P]

- Agent / Ask / Plan tabs; plugin moving to the Copilot harness by default.
- Approvals in Settings > GitHub Copilot > Chat > Auto Approve (changelog only).
- How-to page lists only `.github/copilot-instructions.md`; changelog says
  AGENTS.md, CLAUDE.md and `.instructions.md` also work. Edit mode removed May 2026.
