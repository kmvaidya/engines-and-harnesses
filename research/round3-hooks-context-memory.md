---
url: https://code.visualstudio.com/docs/agent-customization/hooks, https://code.visualstudio.com/docs/agents/reference/hooks-reference, https://code.visualstudio.com/docs/agents/reference/tools-reference, https://code.visualstudio.com/docs/agents/run/agent-harnesses, https://code.visualstudio.com/docs/agents/run/security, https://code.visualstudio.com/docs/agents/reference/workspace-context, https://code.visualstudio.com/docs/agents/reference/ai-settings, https://code.visualstudio.com/docs/enterprise/manage-ai-settings, https://code.visualstudio.com/docs/agents/concepts/context, https://code.visualstudio.com/docs/agents/concepts/agents, https://code.visualstudio.com/docs/agent-customization/custom-instructions, https://code.visualstudio.com/docs/agent-customization/agent-skills, https://code.visualstudio.com/docs/agents/agent-troubleshooting/chat-debug-view, https://code.visualstudio.com/docs/agents/run/memory, https://code.visualstudio.com/updates/v1_109, https://code.visualstudio.com/updates/v1_110, https://docs.github.com/en/copilot/reference/hooks-reference, https://docs.github.com/en/copilot/concepts/agents/hooks, https://docs.github.com/en/copilot/tutorials/copilot-cli-hooks, https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/use-hooks, https://docs.github.com/en/copilot/concepts/security-governance-and-network-settings/content-exclusion, https://docs.github.com/en/copilot/concepts/agents/copilot-memory, https://docs.github.com/en/copilot/how-tos/use-copilot-agents/copilot-memory/manage-for-yourself, https://github.blog/changelog/2026-01-15-agentic-memory-for-github-copilot-is-in-public-preview/, https://github.blog/changelog/2026-03-04-copilot-memory-now-on-by-default-for-pro-and-pro-users-in-public-preview/, https://github.blog/changelog/2026-05-26-copilot-memory-has-more-controls-for-deletion-scope-and-the-copilot-cli/, https://github.blog/changelog/2026-09-25-agentic-autofix-now-uses-copilot-memory/, https://raw.githubusercontent.com/microsoft/vscode-copilot-chat/main/src/extension/tools/common/toolNames.ts
fetched: 2026-10-01
---

# Round 3: hooks, context assembly and memory in VS Code Copilot

Round 3 file. Tags: [P] confirmed against the primary source on 2026-10-01, [R] refuted.

VS Code pages are dated 9/30/2026 (VS Code 1.140). "Local" means the Local
session target (extension host). "Copilot" means the Copilot session target
(Agent Host, same SDK runtime as Copilot CLI). Read alongside
`track1-hooks.md` and `round2-copilot-changes.md` §10.3 and §10.4.

## Q1. Hook file locations and format

**Which reference applies.** [P] "The selected agent harness determines which
hook implementation runs." Local uses "VS Code Local hooks"; Copilot uses the
"Shared Copilot SDK implementation" and the GitHub reference. "Copilot sessions
on Agent Host use the same SDK hook implementation as Copilot CLI. Use the
Copilot CLI sections of the GitHub reference for runtime configuration and
payloads, but verify that the event is available in the selected VS Code
version." [P] "Some harnesses discover the same hook files, such as
`.github/hooks/*.json` or `.claude/settings.json`. This file compatibility does
not make their behavior identical."
(code.visualstudio.com/docs/agent-customization/hooks)

**Local locations** [P] (same page, table):
- Workspace: `.github/hooks/*.json`
- Workspace, Claude format: `.claude/settings.json`, `.claude/settings.local.json`. "Requires `chat.useClaudeHooks`, which is off by default."
- User: `~/.copilot/hooks/*.json`
- User, Claude format: `~/.claude/settings.json` (requires `chat.useClaudeHooks`)
- Custom agent: "`hooks` in `.agent.md` frontmatter". "Runs only for that custom agent in the Local harness."
- Plugin: "`hooks.json` or `hooks/hooks.json`"
- [P] "The `chat.useHooks` setting controls Local hook execution and is on by default." `chat.hookFilesLocations` adds or disables locations.

**Copilot (CLI runtime) locations** [P] (docs.github.com/en/copilot/reference/hooks-reference):
policy dir (`C:\ProgramData\GitHub\Copilot\policy.d\*.json` on Windows, or
registry `HKLM\Software\Policies\GitHub\Copilot`), "`.github/hooks/*.json` in
the repository root", "`~/.copilot/hooks/` on macOS and Linux, or
`%USERPROFILE%\.copilot\hooks\` on Windows", inline `hooks` in
`.github/copilot/settings.json` / `.github/copilot/settings.local.json`,
"Cross-tool `.claude/settings.json` and `.claude/settings.local.json` files in
the repository are also read", `~/.copilot/settings.json`, plugin `hooks.json`.
[P] VS Code: "Copilot sessions on Agent Host use the shared SDK hooks
implementation and load Copilot Policy Hooks. Local sessions do not load SDK
Policy Hooks." (agents/run/agent-harnesses)

**Formats.** [P] Local native format = "PascalCase events without a numeric
`version` property", properties `command`, `windows`, `linux`, `osx`,
`timeout` (default 30 s), `cwd` ("relative to the repository root"), `env`.
Local also accepts the Copilot format ("Numeric `version` property and lower
camel case events ... Maps Copilot event and command property names to the
Local format. Runtime payloads still use the Local schema.") and the Claude
format ("Local parses nested commands but ignores matcher values").
[P] Copilot format: `"version": 1`, camelCase events, `bash` / `powershell` /
`command` ("Cross-platform fallback. Copied to both `bash` and `powershell`
when those fields are absent"), `cwd` ("relative to repository root or
absolute"), `env`, `timeoutSec` (default 30), plus `http` and `prompt` types.

**Minimal complete example, verbatim** [P] (VS Code hooks page, "Create your first Local hook"), `.github/hooks/audit.json`:

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "type": "command",
        "command": "node .github/hooks/log-tool-use.cjs"
      }
    ]
  }
}
```

with `.github/hooks/log-tool-use.cjs`:

```js
const fs = require('node:fs');

let input = '';
process.stdin.setEncoding('utf8');
process.stdin.on('data', chunk => (input += chunk));
process.stdin.on('end', () => {
  const event = JSON.parse(input);
  fs.appendFileSync(
    '.github/hooks/tool-use.log',
    `${event.timestamp} ${event.tool_name}\n`
  );
});
```

[P] "This example also helps you discover the exact Local tool names to use in
validation hooks. Tool names and arguments differ between harnesses."

Managing: [P] "Enter `/hooks` in the chat input", Configure Chat (gear) >
Hooks, **Chat: Configure Hooks**, and "`/create-hook <description>` ... The
generated hook uses `.github/hooks/`."

## Q2. Events

**Local (8 events)** [P] (hooks page table): `SessionStart` ("The first prompt
starts a session."), `UserPromptSubmit`, `PreToolUse`, `PostToolUse` ("After a
tool completes successfully."), `PreCompact`, `SubagentStart`, `SubagentStop`,
`Stop` ("The current agent execution is about to stop.").

**Copilot (CLI runtime, 14 events)** [P] (GitHub hooks reference): `agentStop`,
`errorOccurred`, `notification`, `permissionRequest`, `postToolUse`,
`postToolUseFailure`, `preCompact`, `preToolUse`, `sessionEnd`,
`sessionStart`, `subagentStart`, `subagentStop`, `userPromptSubmitted`,
`userPromptTransformed`. PascalCase "VS Code compatible" names switch the
payload to snake_case. Which of these fire inside VS Code's Agent Host:
**not found**; VS Code says only "verify that the event is available in the
selected VS Code version."

**Preview status** [P]: "The VS Code hooks experience is in Preview.
Individual provider implementations might have a different lifecycle status.
For example, hooks in the Copilot SDK are generally available." "Agent-scoped
hooks are in Preview and are supported only by the Local harness." Enterprise
page: "The SDK hooks implementation is generally available (GA), while the VS
Code hooks surface remains in Preview during the transition."
No per-event Preview flags found.

## Q3. PreToolUse

**Local input** [P] (agents/reference/hooks-reference): common fields
`timestamp`, `cwd`, `session_id`, `hook_event_name`, `transcript_path`, plus
`tool_name` ("Name of the Local tool"), `tool_input` ("Arguments for the tool
call"), `tool_use_id`.

**Local deny** [P], two ways:
- stdout `{"hookSpecificOutput": {"hookEventName": "PreToolUse", "permissionDecision": "deny", "permissionDecisionReason": "...", "additionalContext": "..."}}`; values `"allow"`, `"deny"`, `"ask"`; `updatedInput` can rewrite arguments. "When multiple hooks return a permission decision for the same tool call, the most restrictive decision wins."
- Exit code: "`2` | Treat stderr as a blocking error and provide it to the model." "Any other value | Show a non-blocking warning to the user and continue processing."

**Copilot input and deny** [P] (GitHub reference): camelCase input
`toolName`, `toolArgs`; PascalCase input `tool_name`, `tool_input` ("parsed
from JSON string when possible"). Output is top level:
`permissionDecision` (`"allow"`, `"deny"`, `"ask"`),
`permissionDecisionReason` ("Required when decision is `"deny"`"),
`modifiedArgs`. Exit 2: "For `permissionRequest` and `preToolUse`, exit `2` is
treated as a deny". The tutorial adds: "`toolArgs`: A JSON string containing
that tool's arguments ... your script must parse it before reading fields like
`command`." (docs.github.com/en/copilot/tutorials/copilot-cli-hooks)

**Matchers.**
- Local: [P] the native command-property table has no `matcher` field, and for Claude-format files "Local ignores matcher values, so every command for the event runs." Filter inside the script on `tool_name`.
- Copilot: [P] "Optional regex tested against `toolName` ... compiled as `^(?:PATTERN)$`". With PascalCase `PreToolUse`, "Claude's matcher semantics" apply and "Payloads for PascalCase `PreToolUse` report `tool_name` as the Claude tool name (for example, `Bash`, not `bash`)."

**Tool names.**
- Copilot [P] (reference table): `bash` and `powershell` ("Execute shell commands (Windows)"), `view` ("Read file contents"), `create`, `edit`, `glob`, `grep`, `web_fetch`, `task`, `ask_user`. Claude mapping table adds `str_replace_editor`, `apply_patch` (Edit), `rg` (Grep), `web_search`, `update_todo`.
- Local: **not found in the docs.** The tools reference lists only `#` picker names (`#read/readFile`, `#edit/createFile`, `#edit/editFiles`, `#execute/runInTerminal`, `#search/fileSearch`, `#search/textSearch`, `#search/codebase`), not the `tool_name` string in the hook payload. The docs say: "Replace `<tool-name>` with the exact Local tool name. Do not copy a tool name from another harness" and use the audit hook or agent debug logs to find it. Outside the docs, the open-source extension enum (toolNames.ts, last commit 2026-03-31) has `run_in_terminal`, `read_file`, `create_file`, `replace_string_in_file`, `multi_replace_string_in_file`, `insert_edit_into_file`, `apply_patch`, `file_search`, `grep_search`, `semantic_search`, `list_dir`, `memory`. Source code, not docs: confirm with the audit hook before putting these on a slide.

**Can PreToolUse deny a file read?** Yes, on both harnesses, because reads are
tool calls (`view` / Local read tool) and PreToolUse "fires before the agent
invokes a tool" [P]. **Documented example of blocking `.env` reads: not found.**
The documented examples block destructive shell commands (VS Code security
page: "block dangerous commands (for example, `rm -rf` or `DROP TABLE`)") and
the GitHub tutorial's bash deny rules. The nearest documented `.env` guidance
is for edits only: `chat.tools.edits.autoApprove` with `"**/.env": false` "to
require manual approval for edits to sensitive files" [P] (agents/run/security).

**Gaps (inference from the documented mechanics, not stated by the docs):**
1. Terminal reads (`cat .env`, `Get-Content .env`, `type .env`) go through the shell tool, so the hook only sees a command string. String matching catches plain paths but not globs, variables or encoded paths.
2. Search tools: a grep or semantic search across the workspace can return lines from a secret file without naming it in the arguments. [P] "every match returned becomes part of the conversation context, even if the agent never opens the file." (workspace-context)
3. User-supplied context never passes through a tool call: implicit context ("The currently selected text in the active editor"), `#file` attachments, and [P] "`.gitignore` is bypassed if you have a file open or have text selected within an ignored file."
4. Local fails open on hook errors ("Any other value | ... continue processing"), so a crashing guard script lets the call through. Copilot fails closed on crashes but [P] "Command hook timeouts are always fail-open, even for `preToolUse`".
5. Agent Host limitation [P]: "Copilot sessions don't have access to every VS Code built-in or extension-provided tool", so tool sets differ by target.

## Q4. Two working hooks (Windows-friendly)

Design choices, each tied to a documented fact:
- **Node scripts, one `command`.** VS Code's own examples use `node .github/hooks/*.cjs`. In the Copilot format, `command` is "Copied to both `bash` and `powershell`", so the same line runs on Windows and Linux. [P] GitHub's Windows examples "require you to have PowerShell 7.0 or later installed and in your PATH" (use-hooks how-to). Node avoids writing two scripts.
- **Copilot format (`version: 1`, camelCase).** The Copilot harness reads it natively and Local "Maps Copilot event and command property names to the Local format" [P]. One file serves both targets.
- **Read both payload shapes.** Local sends `tool_input` (object); Copilot camelCase sends `toolArgs` (may be a JSON string).
- **Deny with exit 2 plus stderr and stdout JSON.** Exit 2 blocks on both harnesses [P]. Stdout carries the top-level Copilot fields and the Local `hookSpecificOutput`. Whether each harness tolerates the other's extra fields is not documented; exit 2 makes the outcome the same either way.
- **Match on arguments, not tool names.** Local tool names are undocumented, so the push guard checks any `command` argument and the path guard scans all arguments.

`.github/hooks/guardrails.json`:

```json
{
  "version": 1,
  "hooks": {
    "preToolUse": [
      { "type": "command", "cwd": ".github/hooks", "command": "node block-git-push.cjs", "timeoutSec": 10 },
      { "type": "command", "cwd": ".github/hooks", "command": "node protect-paths.cjs", "timeoutSec": 10 }
    ]
  }
}
```

`.github/hooks/block-git-push.cjs`:

```js
// Deny any shell command that runs `git push`.
let raw = '';
process.stdin.on('data', c => (raw += c));
process.stdin.on('end', () => {
  const ev = JSON.parse(raw);
  let args = ev.tool_input ?? ev.toolArgs ?? {};          // Local shape ?? Copilot shape
  if (typeof args === 'string') { try { args = JSON.parse(args); } catch {} }
  const cmd = typeof args.command === 'string' ? args.command : '';
  if (/\bgit\b[^\n;&|]*\bpush\b/i.test(cmd)) {
    const reason = 'Policy: the agent may not run git push. Stop and ask the user to push.';
    process.stdout.write(JSON.stringify({
      permissionDecision: 'deny', permissionDecisionReason: reason,             // Copilot harness
      hookSpecificOutput: { hookEventName: 'PreToolUse',
        permissionDecision: 'deny', permissionDecisionReason: reason },         // Local harness
    }));
    process.stderr.write(reason);
    process.exit(2);                                         // exit 2 blocks in both harnesses
  }
  process.exit(0);                                           // no opinion
});
```

`.github/hooks/protect-paths.cjs`:

```js
// Deny any tool call whose arguments name a protected path.
const PROTECTED = [
  /(^|[\/\s"'`=])\.env(\.(?!example\b)[\w.-]+)?(?=$|[\s"'`;|&)\/])/i, // .env, .env.local (not .env.example)
  /(^|[\/\s"'`])secrets\//i,                                          // anything under secrets/
  /\.(pem|key|pfx)\b/i,                                               // key files
];
let raw = '';
process.stdin.on('data', c => (raw += c));
process.stdin.on('end', () => {
  const ev = JSON.parse(raw);
  const args = ev.tool_input ?? ev.toolArgs ?? {};          // Local shape ?? Copilot shape
  const text = (typeof args === 'string' ? args : JSON.stringify(args)).replace(/\\+/g, '/');
  if (PROTECTED.some(re => re.test(text))) {
    const reason = 'Policy: this path is protected (.env, secrets/, key files). Do not read, search or print it.';
    process.stdout.write(JSON.stringify({
      permissionDecision: 'deny', permissionDecisionReason: reason,
      hookSpecificOutput: { hookEventName: 'PreToolUse',
        permissionDecision: 'deny', permissionDecisionReason: reason },
    }));
    process.stderr.write(reason);
    process.exit(2);
  }
  process.exit(0);
});
```

Tested locally (Node 24, Windows) against synthetic payloads in both shapes:
blocks `git push`, `git -C . push`, `git push origin HEAD --force` (as a
`powershell` toolArgs JSON string), `C:\repo\.env`, `.env.production`,
`Get-Content .env`, `secrets/prod.json`, `certs\server.pem`, and a grep with
`includePattern: "**/.env"`. Allows `git pull`, `.env.example`,
`src/environment.ts`, and a `create_file` whose *content* mentions "git push".
**Not tested inside VS Code**: the Local field names `command` and `filePath`
come from the source enum, not the docs. Run the audit hook from Q1 once to
confirm.

Windows notes [P]:
- Local picks the OS override "from the extension host platform. In Remote Development windows, this platform might differ from the operating system that displays the VS Code UI."
- Copilot harness on Windows uses the `powershell` tool name, not `bash`, so a guard that checks `toolName == "bash"` misses every Windows shell call (see Disagreements).
- In the Copilot harness, a crash or a wrong `cwd` makes `preToolUse` deny *every* tool call ("a crash or non-zero exit ... denies the tool call"). In Local the same failure only warns. Test the hook before committing it.
- Hooks are a guardrail, not a boundary. For enforced denial, admins can set managed `"deny": ["Read(...)"]` and `"ask": ["Shell(git push *)"]` rules (Q8).

## Q5. PostToolUse: run a formatter or tests and feed results back

- Local [P]: input adds `tool_response`. Output: `"decision": "block"` with `reason` ("Reason provided to the model when processing is blocked") and/or `hookSpecificOutput.additionalContext` ("Additional context for the model"). Docs example: `{"decision": "block", "reason": "Post-processing validation failed.", "hookSpecificOutput": {"hookEventName": "PostToolUse", "additionalContext": "The edited file has lint errors."}}`. Formatter example in the docs: `"PostToolUse": [{"type": "command", "command": "npx prettier --write ."}]`. Exit 2 also sends stderr to the model.
- Copilot [P]: output `additionalContext` ("appended to `textResultForLlm` so the model sees it after the tool output on the same turn ... capped at 10 KB") and `modifiedResult` (replaces the tool result). `matcher` works, for example `"matcher": "bash|edit"`. `postToolUseFailure` is separate: "can provide recovery guidance via `additionalContext` (exit code `2` for command hooks)".
- So yes: run lint or tests on edit tools and return the output as `additionalContext`. Local has no matcher, so filter on `tool_name` in the script.

## Q6. Injecting context; blocking Stop

- **SessionStart: yes, both.** Local [P]: `{"hookSpecificOutput": {"hookEventName": "SessionStart", "additionalContext": "Project: my-app 2.1.0 | Branch: main"}}`, "Context added to the conversation." Copilot [P]: top-level `{ additionalContext?: string }`; "Only `additionalContext` is consumed for `sessionStart`". Copilot CLI also has `prompt` hooks that auto-submit text, "only supported on `sessionStart`" and "fire only for new interactive sessions" (CLI only).
- **UserPromptSubmit: no context injection via command hooks.** Local [P]: "The hook supports the common output" (`continue`, `stopReason`, `systemMessage`; no `additionalContext` listed). Copilot [P]: "Command and HTTP config-file `userPromptSubmitted` hooks have their output dropped, including `modifiedPrompt`." `userPromptTransformed` can rewrite model-facing content (Copilot runtime).
- **For a "the onboarding doc is stale" reminder**, use SessionStart. Script outline: compare the doc's last git commit date with a threshold and print the JSON above. Local's `systemMessage` shows a warning to the *user* only.
- **SubagentStart** [P]: both harnesses can add `additionalContext` to the subagent (Copilot: "prepended to the subagent's first user message").
- **Stop: yes, both can block and give the next instruction.** Local [P]: `{"hookSpecificOutput": {"hookEventName": "Stop", "decision": "block", "reason": "Run the test suite before finishing."}}`; "`reason` ... Required when `decision` is `"block"`"; "the additional turns consume AI credits. Check `stop_hook_active` to prevent the agent from continuing indefinitely." Copilot [P]: `agentStop` top-level `decision: "block"` "forces another agent turn using `reason` as the prompt"; "After 8 consecutive `block` continuations, the CLI overrides the hook and ends the turn anyway". Local runaway cap: **not found**.

## Q7. Failure behaviour and trust

- **Local** [P]: exit `0` processes stdout; `2` blocks with stderr to the model; "Any other value | Show a non-blocking warning to the user and continue processing." So errors fail **open**, including PreToolUse. Default timeout 30 s; what Local does on timeout: **not found**. Debugging: Output panel "GitHub Copilot Chat Hooks channel".
- **Copilot** [P]: "Command `preToolUse` hooks are fail-closed on errors". "Command hook timeouts are always fail-open, even for `preToolUse` and admin-deployed policy hooks". "HTTP `preToolUse` hooks are fail-open". Other events: "non-zero exits and timeouts are logged and skipped".
- **Trust** [P]: "Workspace hook files are subject to Workspace Trust." "Agent-scoped hooks require `chat.useHooks` and a trusted workspace." Security page: "opening untrusted projects in restricted mode disables agents". GitHub: policy hooks "are available regardless of folder trust state" (implies other sources depend on it). **A prompt that asks the user to approve repo hooks before they first run: not found.**
- **Admin controls** [P]: `ChatHooks` policy disables Local hooks; "`ChatHooks` applies only to the Local harness." `allowManagedHooksOnly` (from 1.132) "allows hooks only from managed sources and plugins force-enabled by policy." The Local settings `chat.useHooks`, `chat.hookFilesLocations` and `chat.useClaudeHooks` "do not configure Copilot, Claude, or Codex hook execution."

## Q8. Other ways to stop the agent reading files

- **Content exclusion** [P]: "Content exclusion is currently not supported in Edit and Agent modes of Copilot Chat in Visual Studio Code and other editors." The table marks VS Code Edit and Agent as "Not supported"; the Copilot app and CLI as supported. Whether it applies to VS Code Copilot-target (CLI runtime) sessions: **not found**. Business/Enterprise only.
- **`files.exclude` / `search.exclude` / `.gitignore`** [P]: `.gitignore` "excludes files from text search, grep, and the semantic index"; `files.exclude` "hides files from the Explorer and excludes them from text search, grep, and the semantic index"; `search.exclude` "excludes files from text search and grep". The page sells these for "search relevance" and token cost, not security. It does not say they block a direct file read, and ".gitignore is bypassed if you have a file open".
- **`.copilotignore`: not found** in any fetched VS Code or GitHub page.
- **Managed permissions (Copilot target only, enterprise)** [P]: `managed-settings.json` example `"deny": ["Read(~/.config/secret.txt)", ...]`, `"ask": [..., "Shell(git push *)"]`; "`deny` blocks a matching operation with no approval option." "These settings apply only to users who receive Copilot enterprise managed settings and to Copilot sessions that use Agent Host." No user-level or workspace equivalent found for VS Code.
- **Terminal sandbox** [P]: `chat.agent.sandbox.fileSystem.windows` (Preview) "Supports `allowRead`, `allowWrite`, and `denyRead` properties" for "sandboxed agent commands"; Windows sandboxing itself (`chat.agent.sandbox.enabledWindows`) is Experimental, default `off`. Covers terminal commands only.
- **Edits only** [P]: `chat.tools.edits.autoApprove` `"**/.env": false` requires approval for edits, not reads.
- Read scope [P]: `github.copilot.chat.additionalReadAccessFolders` "Grant read-only access to additional folders outside the current workspace for built-in agent tools."

## Q9. What goes into context, and how to see it

- [P] (agents/concepts/context) "Each time the agent sends a request to the language model, VS Code assembles a prompt from multiple sources:" System instructions ("built-in guidelines that define the agent's behavior"); Customizations ("custom agents, skills, and custom instructions"); User message; Conversation history; Implicit context ("the file you're editing, your current selection, visible errors, and git state"); Explicit references (`#`-mentions); Tool outputs.
- **Order: not documented.** The list is not described as an order. [P] "Applicable instruction sources are additive. Do not depend on a file order or precedence rule to resolve conflicts because discovery and merge behavior can differ by harness." (custom-instructions)
- Placement clues [P] (chat-debug-view): "inspect the System prompt for custom instructions and the User prompt for an invoked prompt file"; the debug view shows whether a tool "appears in the available tool definitions".
- Instructions [P]: project files are "automatically included according to the selected harness"; `.instructions.md` attached when "its `applyTo` pattern matches a file that the agent creates or modifies", or loaded on demand by `description`.
- Skills [P]: "Copilot reads the skill's `name` and `description` from the YAML frontmatter", then loads the `SKILL.md` body when matched, then extra files "only when it references them."
- Memory [P]: user memory "The first 200 lines are automatically loaded into the agent's context at the start of every session."
- Implicit context detail [P]: "When you use the Ask agent, the contents of the active file." "When you use Agent, the active file as a suggested attachment that you can add to the context."
- Compaction [P]: "When a conversation approaches the limit, VS Code automatically compacts older parts of the conversation into a summary"; manual `/compact`.
- **Seeing the assembled request** [P]: **Developer: Show Chat Debug View** (sections System prompt, User prompt, Context, Response, Tool responses). Agent Debug Logs (Preview): "Expand an event to inspect details such as the system prompt for a model request". Agent Host sessions need `chat.agentHost.agentDebugLog.enabled` (experimental) turned on first; "Capture is not retroactive." Also `/troubleshoot Which customizations were loaded, and did any fail?`.

## Q10. Memory

**Two different systems.**
1. **VS Code memory tool (local files)** [P] (agents/run/memory): "a built-in agent tool that allows agents to save and recall notes as they work." "User, repository, and session memory are stored locally on your machine." Scopes: User `/memories/` (across workspaces), Repository `/memories/repo/` ("workspace-scoped"), Session `/memories/session/` (current conversation; the Plan agent keeps `plan.md` there). Store with "ask the agent to remember something"; view with **Chat: Show Memory Files**; delete all with **Chat: Clear All Memory Files**; "To update or delete an individual memory file, ask the agent." Concepts page: "When the memory tool is available..." Enable setting, default state, and which session targets offer it: **not found** in the settings reference. No expiry documented.
2. **GitHub Copilot Memory (server side)** [P] (docs.github.com concept page): public preview; repository-level facts "stored with citations", "checks those citations against the current branch"; user-level preferences; "any stored fact or preference that goes unused is automatically deleted after 28 days. The 28-day timer may reset whenever Copilot successfully validates and uses an entry." "Copilot Memory is currently used by Copilot cloud agent, Copilot code review, Copilot CLI, and agentic autofix." "For individual plans, it's on by default. For enterprise- and organization-managed plans, an administrator must enable the policy first, and then individual users can opt out."
   - View/delete [P]: personal preferences at Copilot settings > Memory; repo facts at "Settings ... Copilot, then click Memory" (repo owners); enable/disable under Copilot settings "Features". Changelog 2026-05-26: a repo-level off switch, CLI `/memory on|off|show`, and the `store_memory` permission prompt "explicitly states whether the entry will be a user-level preference ... or a repository-level fact".

**Relationship in VS Code.** VS Code 1.109 release notes [P]: "Copilot Memory (Preview) ... With the new memory tool, your chat can now access and update Copilot Memory directly ... Enable the memory tool by setting `github.copilot.chat.copilotMemory.enabled` to `true` ... You can view and manage all your memories from GitHub's Copilot settings." The current VS Code memory page and settings reference (9/30/2026) describe only local files and do not list that setting. GitHub's surface list does not name VS Code. Whether VS Code's Copilot target, which runs the CLI runtime, reads or writes GitHub Copilot Memory: **not found**. Safe slide wording: "VS Code's memory tool writes local files; GitHub Copilot Memory is the server-side, cited, 28-day store used by cloud agent, code review, CLI and autofix."

## Disagreements and stale pages

1. **GitHub tutorial PowerShell bug.** `pre-tool-policy.ps1` exits early with `if ($toolName -ne "bash") { exit 0 }`, but the reference says Windows shell calls are `powershell` ("Execute shell commands (Windows)"). On Windows the tutorial's deny rules never fire. (copilot-cli-hooks tutorial vs hooks-reference)
2. **`toolArgs` type.** Tutorial: "`toolArgs`: A JSON string". Reference: `toolArgs: unknown`; PascalCase `tool_input` "parsed from JSON string when possible". Handle both.
3. **postToolUse scope.** GitHub concept page: "Executed after a tool completes execution (whether successful or failed)." Reference: "After each tool completes successfully", with a separate `postToolUseFailure`. Use the reference.
4. **GitHub surfaces.** Reference: "Hooks are supported in two Copilot surfaces: Copilot CLI and Copilot cloud agent." VS Code: Copilot sessions use "the same SDK hook implementation as Copilot CLI." Neither lists which events fire in VS Code.
5. **Stop output shape differs.** Local nests `decision` inside `hookSpecificOutput` for `Stop` but uses top-level `decision` for `SubagentStop`. Copilot uses top-level for both.
6. **Fail mode differs.** Local: errors are "non-blocking"; Copilot: `preToolUse` crashes deny. Same script, opposite outcome on a bug.
7. **Tool name table.** The reference's matching table lists 10 tools; the Claude mapping table also names `str_replace_editor`, `apply_patch`, `rg`, `web_search`, `update_todo`. `track1-hooks.md` merged them into one list.
8. [R] Round 2 §10.3 said the Local harness "ignores matcher values" in general. The current page says this only for Claude-format files; the native Local format simply has no `matcher` property. Practical result is the same: filter inside the script.
9. **Memory.** VS Code 1.109 notes tie the memory tool to GitHub Copilot Memory via `github.copilot.chat.copilotMemory.enabled`. The current docs describe a local-file tool only and omit the setting. The Jan 15 changelog calls memories "Repository-specific"; current docs add user-level preferences.
10. GitHub concept page example path "`~/.github/hooks/project-hooks.json` within a repository" mixes a home path with a repo path; the reference says `.github/hooks/*.json` in the repo root.
