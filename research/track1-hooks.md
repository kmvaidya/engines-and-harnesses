---
url: https://docs.github.com/en/copilot/reference/hooks-reference, https://docs.github.com/en/copilot/concepts/agents/hooks, https://code.visualstudio.com/docs/agent-customization/hooks
fetched: 2026-08-12
---

# Hooks — YES, they exist on the Copilot surface now (CLI + cloud agent + VS Code preview)

This is one of the biggest changes vs 2024-2025: Copilot now has a full lifecycle-hooks system, closely mirroring Claude Code's hooks (VS Code even documents a "Claude-compatible" PascalCase event format and reads `.claude/settings.json`).

## Where hooks run

- **Copilot CLI** — all events, on the local machine. (https://docs.github.com/en/copilot/concepts/agents/hooks)
- **Copilot cloud agent** — subset of events, in its ephemeral Linux sandbox; only `bash`/`command` entries honored; only `.github/hooks/*.json` is read. (https://docs.github.com/en/copilot/reference/hooks-reference)
- **VS Code** — "Agent hooks are currently in Preview." (https://code.visualstudio.com/docs/agent-customization/hooks)

## Config file locations

- Repository: **`.github/hooks/*.json`** (applies to all Copilot agents in the repo)
- Personal (CLI): **`~/.copilot/hooks/*.json`** (`%USERPROFILE%\.copilot\hooks\` on Windows)
- Policy (admin, CLI): `/etc/github-copilot/policy.d/*.json` (Linux/macOS) or `C:\ProgramData\GitHub\Copilot\policy.d\*.json` (Windows) — policy hooks ALWAYS run, cannot be disabled
- Repo settings: `.github/copilot/settings.json` / `.github/copilot/settings.local.json`; user: `~/.copilot/settings.json`
- VS Code additionally reads: `.claude/settings.json`, `.claude/settings.local.json`, `~/.claude/settings.json`, `~/.copilot/hooks`, plugin `hooks.json`, and the `hooks:` frontmatter of `.agent.md` files (agent-scoped hooks, preview, setting `chat.useCustomAgentHooks`); paths configurable via `chat.hookFilesLocations`.

## Events (exact names, from the hooks reference)

camelCase (CLI/cloud agent): `sessionStart`, `sessionEnd`, `userPromptSubmitted`, `userPromptTransformed`, `preToolUse`, `postToolUse`, `postToolUseFailure`, `agentStop`, `subagentStart`, `subagentStop`, `errorOccurred`, `preCompact`, `notification`, `permissionRequest`

PascalCase ("VS Code compatible", matches Claude Code): `SessionStart`, `SessionEnd`, `UserPromptSubmit`, `PreToolUse`, `PostToolUse`, `PostToolUseFailure`, `Stop`, `SubagentStop`, `ErrorOccurred`, `PreCompact`, `Notification`, `PermissionRequest`

`notification` and `permissionRequest` are CLI-only (cloud agent pre-approves tools; `"ask"` is treated as `"deny"` there).

## Hook types

1. `command` — with `bash` / `powershell` / `command` (cross-platform fallback), `cwd`, `env`, `timeoutSec` (default 30)
2. `http` — POST payload to a URL (`url`, `headers`, `allowedEnvVars`, `timeoutSec`); fail-open on all errors
3. `prompt` — injects a user message/slash command (CLI, new interactive sessions only)

## Decision control (the power feature)

`preToolUse` output:

```typescript
{
  permissionDecision: "allow" | "deny" | "ask";
  permissionDecisionReason?: string;  // Required for "deny"
  modifiedArgs?: object;              // Substitute tool arguments
}
```

`agentStop`/`Stop` output can `{"decision": "block", "reason": "..."}` to force the agent to continue. `subagentStop` can rewrite the subagent's response via `modifiedResponse`. `postToolUse` can rewrite tool results (`modifiedResult`) or append `additionalContext`.

Exit codes (command hooks): `0` = success (stdout parsed as JSON); `2` = warning by default but deny for `preToolUse`/`permissionRequest`; other non-zero = fail-open EXCEPT `preToolUse` which **fails closed**; timeout always fails OPEN.

## Matchers

Optional regex `matcher` (compiled as `^(?:PATTERN)$`) on `preToolUse`, `postToolUse`, `permissionRequest`, `subagentStart`, `preCompact`, `notification`. Tool names for matching: `ask_user`, `bash`, `create`, `edit`, `glob`, `grep`, `powershell`, `task`, `view`, `web_fetch`, `web_search`, `update_todo`, `rg`, `str_replace_editor`, `apply_patch`.
NOTE: VS Code docs say "Currently, VS Code ignores matcher values, so hooks run on all tool invocations regardless of the matcher."

## Copy-paste example (verbatim from hooks reference)

```json
{
  "version": 1,
  "disableAllHooks": false,
  "hooks": {
    "preToolUse": [
      {
        "type": "command",
        "matcher": "bash",
        "bash": "echo '{\"permissionDecision\": \"allow\"}'",
        "timeoutSec": 10
      },
      {
        "type": "http",
        "url": "https://policy.example.com/check",
        "headers": { "Authorization": "Bearer token" },
        "timeoutSec": 5
      }
    ],
    "postToolUse": [
      {
        "type": "command",
        "bash": "echo '{\"additionalContext\": \"Tool executed successfully\"}'",
        "cwd": "/workspace"
      }
    ],
    "sessionStart": [
      {
        "type": "prompt",
        "prompt": "Help me refactor this code"
      }
    ],
    "agentStop": [
      {
        "type": "command",
        "bash": "echo '{\"decision\": \"allow\"}'",
        "timeoutSec": 30
      }
    ]
  }
}
```

VS Code example — block dangerous commands (verbatim):

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "type": "command",
        "command": "./scripts/block-dangerous.sh",
        "timeoutSec": 5
      }
    ]
  }
}
```

with script output:

```json
{
  "hookSpecificOutput": {
    "permissionDecision": "deny",
    "permissionDecisionReason": "Destructive command blocked by security policy"
  }
}
```

VS Code example — auto-format after edits (verbatim):

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "type": "command",
        "command": "./scripts/format-changed-files.sh",
        "windows": "powershell -File scripts\\format-changed-files.ps1",
        "timeout": 30
      }
    ]
  }
}
```

## Cloud-agent environment constraints (from hooks reference)

| Aspect | Details |
|---|---|
| OS | Linux only; `bash`/`command` only |
| Working dir | `/workspace` (cloned repo) or `/root` |
| Filesystem | Ephemeral, discarded when job ends |
| Network | Restricted firewall; GitHub/Copilot endpoints only by default |
| Env vars | `GITHUB_COPILOT_API_TOKEN`, `GITHUB_COPILOT_GIT_TOKEN`, `COPILOT_AGENT_PROMPT` set; `GITHUB_TOKEN` NOT set |
| Interactivity | None; no permission dialogs (`ask` → `deny`) |

## Perf / security guidance (concepts page)

- Hooks run synchronously and block the agent; docs: "Keep hook execution time under 5 seconds when possible."
- Validate/sanitize inputs, shell-escape, never log secrets, set timeouts.
- VS Code: recommend `chat.tools.edits.autoApprove` OFF so the agent can't edit its own hook scripts ("If agents can edit hook scripts, they can modify and execute their own code").

## Progress messages (command hooks)

```bash
echo '{"type": "progress", "message": "Processing..."}'
echo '{"type": "progress", "message": "Finalizing...", "temporary": true}'
echo '{"permissionDecision": "allow"}'
```

## Kill switch

```json
{ "version": 1, "disableAllHooks": true, "hooks": {} }
```
(Disables that file's hooks; policy hooks always run.)
