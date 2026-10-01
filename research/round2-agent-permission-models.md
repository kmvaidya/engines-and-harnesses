---
url: https://code.claude.com/docs/en/permissions, https://code.claude.com/docs/en/permission-modes, https://code.claude.com/docs/en/sandboxing, https://code.claude.com/docs/en/agent-sdk/permissions, https://code.claude.com/docs/en/agent-sdk/user-input, https://code.claude.com/docs/en/agent-sdk/secure-deployment, https://code.claude.com/docs/en/managed-settings, https://code.claude.com/docs/en/hooks, https://code.claude.com/docs/en/monitoring-usage, https://code.claude.com/docs/en/env-vars, https://code.claude.com/docs/en/security, https://learn.chatgpt.com/docs/agent-approvals-security, https://learn.chatgpt.com/docs/sandboxing, https://learn.chatgpt.com/docs/enterprise/managed-configuration, https://learn.chatgpt.com/docs/config-file/config-reference, https://learn.chatgpt.com/docs/config-file/config-advanced, https://learn.chatgpt.com/docs/environments/cloud-environments, https://raw.githubusercontent.com/openai/codex/main/codex-rs/protocol/src/config_types.rs, https://developers.openai.com/api/docs/guides/agents/sandboxes, https://developers.openai.com/api/docs/guides/agents/guardrails-approvals, https://developers.openai.com/api/docs/guides/agents-api/environments/security, https://github.com/openai/openai-agents-python/blob/main/docs/human_in_the_loop.md, https://github.com/openai/openai-agents-python/blob/main/docs/sandbox/guide.md, https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/configure-secrets-and-variables, https://docs.github.com/en/copilot/concepts/agents/cloud-agent/about-cloud-agent, https://docs.github.com/en/copilot/concepts/security-governance-and-network-settings/risks-and-mitigations, https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/customize-the-firewall, https://docs.github.com/en/copilot/concepts/security-governance-and-network-settings/about-cloud-and-local-sandboxes, https://docs.github.com/en/copilot/concepts/agents/about-copilot-cli, https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-command-reference, https://docs.github.com/en/copilot/how-tos/copilot-cli/set-up-copilot-cli/configure-copilot-cli
fetched: 2026-09-30
---

# Agent permission models and secrets handling

Round 2 file, new topic. How four agent harnesses handle approvals,
sandboxing, admin lock-down and secrets, read from vendor docs on 2026-09-30.
Tags: **[P]** confirmed against the primary source on 2026-09-30, **[R]**
refuted. No page showed a publish or update date, so treat every setting name
as true for the versions documented on that day.

Things most likely to surprise a bank audience:

1. **Every harness passes secrets to the agent by default.** Claude Code
   inherits the parent environment and has no built-in deny list; Codex keeps
   KEY/SECRET/TOKEN variables unless configured otherwise; the Copilot cloud
   agent receives its Agents secrets as environment variables.
2. **Claude Code now starts in `auto` mode** (classifier-reviewed actions)
   for interactive sessions from v2.1.283. Admins can turn it off with
   `disableAutoMode`.
3. **Codex retired the `untrusted` approval policy**, and `on-failure` is
   deprecated. Older guides that use them are stale.
4. **Copilot CLI uses the same lock key as Claude Code**
   (`permissions.disableBypassPermissionsMode`) to suppress `--allow-all` and
   `--yolo`.
5. **The OpenAI Agents SDK local sandbox does not confine anything on
   Linux.**

## Comparison

| Harness | Approval modes | Sandbox mechanism | Network default | Admin lock-down | Secrets handling |
|---|---|---|---|---|---|
| Claude Agent SDK / Claude Code | `default` (Manual), `acceptEdits`, `plan`, `auto`, `dontAsk`, `bypassPermissions`; allow/ask/deny rules, `canUseTool` callback, `PreToolUse` hooks | Opt-in Bash sandbox: Seatbelt (macOS), bubblewrap (Linux, WSL2) with optional seccomp; native Windows not supported | Sandbox "pre-allows no domains by default", prompts per new domain | Managed settings that user, project and CLI settings cannot override: `disableBypassPermissionsMode`, `disableAutoMode`, `allowManagedPermissionRulesOnly`, `allowManagedDomainsOnly` | Proxy pattern recommended; `sandbox.credentials` deny/mask; `CLAUDE_CODE_SUBPROCESS_ENV_SCRUB`; no built-in deny list |
| OpenAI Codex CLI | `approval_policy`: `on-request`, `never`, `granular` (`untrusted` retired, `on-failure` deprecated); optional `approvals_reviewer = "auto_review"` | `sandbox_mode`: `read-only`, `workspace-write`, `danger-full-access`; Seatbelt (macOS), bwrap + seccomp (Linux), `elevated`/`unelevated` (Windows) | Off: "By default, the agent runs with network access turned off." | `requirements.toml`, "admin-enforced constraints that users can't override": `allowed_approval_policies`, `allowed_sandbox_modes`, `allowed_permission_profiles` | `shell_environment_policy`; KEY/SECRET/TOKEN exclusion off by default; cloud "network secrets" use placeholders |
| OpenAI Agents SDK sandbox agents | Per-tool `needs_approval`; run pauses with `interruptions`, resumes from `RunState`; input, output and tool guardrails | Depends on backend; `UnixLocalSandboxClient` gives no OS confinement on Linux | Set by the backend, not the SDK | None in the SDK; you build it | "Treat sandbox credentials as runtime configuration, not prompt content"; hosted sandboxes use placeholders plus a proxy |
| GitHub Copilot cloud agent | No per-tool prompts; MCP tools run "autonomously"; humans gate merges and Actions runs | Ephemeral GitHub Actions environment plus firewall | Firewall on, recommended allowlist of registries | Org "Internet access" settings; only users with write access can trigger it | Agents secrets arrive as env vars; `COPILOT_MCP_` ones only reach MCP servers; values masked in logs |
| GitHub Copilot CLI | Per-tool prompt (Yes / Yes for session / No); `--allow-tool`, `--deny-tool`, `--allow-all-tools`, `--allow-all-paths`, `--allow-all-urls`, `--allow-all`, `--yolo`; trusted-directory prompt | Microsoft eXecution Container (MXC): Seatbelt, bubblewrap, Windows BaseContainer; experimental in CLI, public preview overall, off by default | Without the sandbox, commands "reach any network your machine can reach" | `permissions.disableBypassPermissionsMode`; enterprise-managed deny/ask/allow rules (GA Sep 9); managed sandbox floor (`sandbox.enabled`, `failIfUnavailable`); user, server-managed and MDM sources | `--secret-env-vars` redacts named variables from shell and MCP environments; GitHub tokens redacted from output by default |

All cells [P].

## 1. Claude Agent SDK and Claude Code [P]

The SDK and the CLI share one permission engine.

**Evaluation order.** Hooks, then deny rules, then ask rules, then the
permission mode, then allow rules, then the `canUseTool` callback. "Rules are
evaluated in order: deny, then ask, then allow. The first match in that order
determines the outcome, and rule specificity doesn't change the order."
(code.claude.com/docs/en/permissions)

**Modes.**

- `default` (labelled Manual): prompts on first use of each tool.
- `acceptEdits`: auto-approves file edits and `mkdir`, `touch`, `rm`,
  `rmdir`, `mv`, `cp`, `sed` inside the working directories.
- `plan`: never auto-approves file edits.
- `auto`: a classifier model reviews actions. From v2.1.283 it is the
  starting mode for interactive terminal and VS Code sessions on every plan
  and provider.
- `dontAsk`: turns every would-be prompt into a denial and never calls
  `canUseTool`. The SDK docs pair it with `allowedTools` for "a locked-down
  agent".
- `bypassPermissions`: skips prompts. A few actions still prompt in every
  mode, such as explicit ask rules and `rm` of critical paths. "`bypassPermissions`
  offers no protection against prompt injection or unintended actions."
  (code.claude.com/docs/en/permission-modes)

**Rules.** Written as `Tool` or `Tool(specifier)`, e.g. `Bash(npm run *)`,
`Read(./.env)`, `Edit(//secrets/**)`, `WebFetch(domain:example.com)`. A bare
deny such as `disallowed_tools=["Bash"]` removes the tool from the model's
context. Bash argument patterns are fragile: `Bash(rm *)` does not match
`/bin/rm` or `bash -c 'rm ...'`, and the docs say to pair deny rules with the
sandbox network allowlist.

**canUseTool.** Receives the tool name and input; returns allow (optionally
with rewritten input) or deny with a message. The trap: "Auto-approved tools
never reach `canUseTool`." (code.claude.com/docs/en/agent-sdk/permissions)
For checks that must run on every call, use `PreToolUse`: "hooks run before
every other step, and a hook deny applies even in `bypassPermissions` mode."

**Hooks.** `PreToolUse` returns `allow`, `deny`, `ask` or `defer`. Exit code 2
blocks the call, and "even a JSON `permissionDecision` of `"allow"` can't
override it." A hook allow does not skip deny or ask rules. Hook types:
`command`, `http`, `mcp_tool`, `prompt`, `agent`. `allowManagedHooksOnly`
blocks user, project, local and plugin hooks.

**Sandbox.** Covers Bash, PowerShell and Monitor commands and their children.
The built-in Read, Edit and Write tools go through the permission system
instead.

- Writes allowed by default to the working directory, a per-user temp
  directory and added directories.
- Network traffic goes through a proxy outside the sandbox.
- `failIfUnavailable` is off by default: a missing dependency gives a warning
  and **unsandboxed execution**.
- `allowUnsandboxedCommands: false` removes the `dangerouslyDisableSandbox`
  retry escape hatch.
- "Sandboxing reduces risk but is not a complete isolation boundary."
  (code.claude.com/docs/en/sandboxing) The proxy does not inspect TLS by
  default, and sandboxed code "can potentially use domain fronting".
  `network.tlsTerminate` is experimental.

**Managed settings.** `managed-settings.json` in
`/Library/Application Support/ClaudeCode/` (macOS), `/etc/claude-code/`
(Linux) or `C:\Program Files\ClaudeCode\` (Windows), or via MDM, HKLM or
server-managed settings. A managed deny cannot be overridden by
`--allowedTools`. Admins block bypass with
`permissions.disableBypassPermissionsMode: "disable"`. Claude Code refuses
bypass as root or under sudo outside a recognised sandbox. Invalid
restrictive managed keys "fail closed".

**Secrets.**

- "sandboxed Bash commands inherit the parent process environment by
  default, including any credentials set there."
- "There is no built-in credential deny list, so only the files and
  variables you list are restricted."
- `sandbox.credentials` with `mode: "deny"` blocks file reads and unsets
  env vars; `mode: "mask"` hands commands a sentinel that the proxy swaps for
  the real value, only for `injectHosts`. Repo settings cannot set `mask`.
- `CLAUDE_CODE_SUBPROCESS_ENV_SCRUB=1` strips credentials from the Bash tool,
  hooks and MCP stdio servers; on Linux it also isolates the PID namespace.
- The SDK deployment guide recommends a proxy outside the agent that injects
  the key: "The agent can make API calls, but it never sees the credential
  itself." (code.claude.com/docs/en/agent-sdk/secure-deployment)

**Audit.** OpenTelemetry events include `claude_code.user_prompt`,
`claude_code.tool_decision` and `claude_code.tool_result`. Prompt text and
tool details are redacted by default; admins can enable them through the
`env` block in managed settings.

## 2. OpenAI Codex CLI [P]

**Two layers.** The sandbox mode decides what is technically possible; the
approval policy decides when Codex asks.

- Sandbox modes: `read-only`, `workspace-write` ("the default low-friction
  mode for local work"), `danger-full-access` ("removes the filesystem and
  network boundaries").
- Approval policies: `on-request`, `never`, `granular`. "untrusted is
  unsupported, and on-failure is deprecated"
  (learn.chatgpt.com/docs/config-file/config-reference).
- Defaults: version-controlled folders start in `workspace-write` with
  `on-request`; other folders start `read-only`. `.git`, `.agents` and
  `.codex` stay read-only inside writable roots.
- `--dangerously-bypass-approvals-and-sandbox` (alias `--yolo`): "No
  sandbox; no approvals (not recommended)". Web search switches from cached
  to live results under it.

**OS mechanisms.** "macOS uses Seatbelt policies and runs commands using
sandbox-exec"; "Linux uses bwrap plus seccomp by default."
(learn.chatgpt.com/docs/agent-approvals-security) Native Windows: `elevated`
uses "dedicated lower-privilege sandbox users, filesystem permission
boundaries, firewall rules"; `unelevated` uses a restricted token and ACLs
and is "weaker than elevated". Admins can require `elevated` with
`[windows] allowed_sandbox_implementations = ["elevated"]`.

**Network.** "By default, the agent runs with network access turned off."
`sandbox_workspace_write.network_access = true` turns it on; domain rules
apply only when `features.network_proxy` is also on. The DNS rebinding check
"does not eliminate" the risk. The proxy does not filter web search, MCP
connections or app tool calls.

**Auto-review.** `approvals_reviewer = "auto_review"` sends eligible
approval requests to a reviewer agent. Failures "fail closed". Admins can
restrict it with `allowed_approvals_reviewers`.

**Managed config.** `requirements.toml` at `/etc/codex/requirements.toml`
(Unix) or `%ProgramData%\OpenAI\Codex\requirements.toml` (Windows), or via
cloud policy or macOS MDM. The docs' example "blocks --ask-for-approval never
and --sandbox danger-full-access (including --yolo)" using
`allowed_approval_policies` and `allowed_sandbox_modes`
(learn.chatgpt.com/docs/enterprise/managed-configuration). From 0.138.0,
OpenAI prefers `allowed_permission_profiles`. `[experimental_network]` "is
experimental and may change". A `PreToolUse` hook error or timeout "can fail
the hook without blocking the tool": Codex hooks fail open.

**Secrets.** `shell_environment_policy` controls which env vars reach spawned
commands; `inherit = "none"` or `"core"` trims them, and filters can exclude
patterns. The default is permissive: "`ignore_default_excludes` defaults to
true, so Codex doesn't automatically remove variable names containing KEY,
SECRET, or TOKEN." (learn.chatgpt.com/docs/config-file/config-advanced) The
docs do not state the `inherit` default; the source sets it to `All`
(`codex-rs/protocol/src/config_types.rs`). In the cloud: "Programs receive a
placeholder; the proxy substitutes the real value for allowed destinations."

**Audit.** OTel is off by default; when on, it logs approval decisions and
results with prompts redacted by default.

## 3. OpenAI Agents SDK sandbox agents [P]

**Split.** The harness owns "the agent loop, model calls, tool routing,
handoffs, approvals, tracing"; the sandbox is the compute plane. A session
"does not itself guarantee OS-level confinement". On Linux,
`UnixLocalSandboxClient` "runs commands as host processes without adding
OS-level confinement" (openai-agents-python `docs/sandbox/guide.md`).

**Credentials.**

- "Treat sandbox credentials as runtime configuration, not prompt content."
  (developers.openai.com/api/docs/guides/agents/sandboxes)
- Hosted sandboxes: vault secrets appear as placeholders; a network proxy
  supplies the real value for approved hosts.
- "Agent-generated code can read the environment key. Keep your application
  API key outside the environment."
- Serialized state strips cloud mount credentials; "serialized state never
  grants authority by itself."

**Approvals.**

- `needs_approval` on `function_tool`, `Agent.as_tool`, `ShellTool`,
  `ApplyPatchTool`; MCP servers use `require_approval`.
- "Callable approval rules fail closed when the SDK cannot safely inspect
  the arguments."
- For local `ShellTool` and `ApplyPatchTool`, "approval is opt-in:
  `needs_approval` defaults to `False`." Hosted shell does not support it.
- "`RunState.from_json()` and `RunState.from_string()` do not authenticate
  the snapshot or the person submitting it." A paused run saved to storage
  can be tampered with unless you protect it.

**Guardrails.** Input guardrails run only for the first agent, output
guardrails only for the final agent, tool guardrails only on the tools they
are attached to. "Responses API and Agents SDK applications don't
automatically inherit Codex Auto-review."

## 4. GitHub Copilot cloud agent and CLI [P]

**Cloud agent secrets.** "Variables and secrets that you configure are
exposed to Copilot as environment variables, except secrets and variables
prefixed with COPILOT_MCP_, which are only available to MCP servers."

- No access to "GitHub Actions, Codespaces, or Dependabot secrets and
  variables."
- "Secret values are masked in Copilot cloud agent session logs."
- Secrets in the old `copilot` Actions environment were migrated to Agents
  secrets automatically.

**Cloud agent controls.** Only users with write access can trigger it. It
pushes only to its own `copilot/` branch or the PR branch and "cannot
directly run git push". A human must review and merge; Actions workflows wait
for human approval. MCP tools run "autonomously and will not ask you for
approval first", so GitHub recommends allowlisting read-only tools. The
firewall covers only Bash-started processes and "should not be considered a
comprehensive security solution". Commits are signed; session logs and audit
events are available to admins.

**CLI approvals.** The CLI asks whether you trust the launch directory, but
"Scoping of permissions is heuristic and GitHub does not guarantee that all
files outside trusted directories will be protected." `--deny-tool` beats
`--allow-all-tools` and `--allow-tool`. `--allow-all` and `--yolo` equal
`--allow-all-tools --allow-all-paths --allow-all-urls`. Approving a tool "for
the rest of the running session" covers any use of it, for example any `rm`.

**CLI admin lock.** "When permissions.disableBypassPermissionsMode is set to
"disable", all of the command line options that allow all permissions
(--allow-all-tools, --allow-all-paths, --allow-all-urls, --allow-all, --yolo)
are suppressed at startup" (docs.github.com, CLI command reference). A
malformed value is treated as `"disable"`. An MDM policy "cannot be
overridden by account switches".

**Enterprise-managed permissions (GA Sep 9, 2026).** Admins set deny, ask and
allow rules (`Shell(...)`, `Read(...)`, `Edit(...)`, `Domain(...)`) that
"can't be weakened by user or workspace settings, auto-approval, or
previously saved approvals", and "A managed `ask` rule can't be satisfied by
bypass mode". Covers the Copilot app, CLI and VS Code Agent Host sessions,
**not the cloud agent or JetBrains**. Requires CLI v1.0.88 or later to apply
in ACP and `--server` modes. Detail in `round2-copilot-changes.md` §10.1.
Copilot policy hooks fail open on timeout, so these rules, not hooks, are the
hard control.

**CLI sandbox.** MXC: Seatbelt (macOS), bubblewrap (Linux), BaseContainer
(Windows). "Turned off by default". Experimental in the CLI; "Cloud and local
sandboxes for GitHub Copilot are in public preview and subject to change."
On an unsupported host, commands run unsandboxed unless enterprise policy
enforces sandboxing; `failIfUnavailable` makes it mandatory. The proxy is not
enforced on macOS (env vars only) and not available on Windows. Built-in file
tools are not OS-sandboxed and honour the policy "on a best-effort basis".
The Copilot app's local sandbox is covered in `round2-copilot-changes.md` §2.

## 5. What a bank harness should copy

Each point is a pattern at least two vendors document, with sources above.

- **Keep credentials outside the agent boundary and inject them at a
  proxy.** Claude SDK secure deployment, Claude Code `mask`, OpenAI hosted
  sandboxes and Codex cloud network secrets all use a placeholder plus proxy
  substitution.
- **Scrub the environment explicitly, because every default passes secrets
  through.** The knobs: `CLAUDE_CODE_SUBPROCESS_ENV_SCRUB`,
  `shell_environment_policy.inherit = "none"`, Copilot `--secret-env-vars`.
- **Evaluate deny first, and put one check on every call that fails
  closed.** Claude evaluates deny before allow and skips `canUseTool` for
  auto-approved calls, so the always-on check belongs in `PreToolUse`.
  Copilot `--deny-tool` beats allow-all. Agents SDK callables and Codex
  auto-review fail closed. Codex hooks fail open, which is the counterexample.
- **Ship an admin policy layer that bans bypass modes and fails closed when
  malformed.** Claude and Copilot `disableBypassPermissionsMode`; Codex
  `allowed_sandbox_modes` without `danger-full-access`. Claude and Copilot
  both enforce the restrictive value when the policy cannot be read.
- **Make a missing sandbox a hard stop, and do not treat hostname allowlists
  as complete.** Claude and Copilot fall back to unsandboxed execution unless
  `failIfUnavailable` is set. Claude warns about domain fronting; Codex says
  DNS rebinding is not eliminated; Copilot's firewall skips MCP servers.
- **Turn on audit telemetry deliberately, and protect saved approval
  state.** Claude and Codex OTel redact detail by default. Agents SDK
  `RunState` snapshots are not authenticated.

## 6. Open questions

- Native Windows: Claude Code's sandbox does not run there, Codex
  `unelevated` is described as weaker, and Copilot's Windows proxy is
  unavailable. How does each hold up on a Windows-heavy bank fleet?
- The Codex docs do not state the `shell_environment_policy.inherit`
  default; the source says `All`. Check on the release you deploy.
- Classifier approvers (Claude `auto`, Codex `auto_review`): no page gives
  miss rates. What evidence would a model-risk team accept?
- Claude `auto` sends actions for classifier review. The "Server-side
  classifier review" section was not read in full, so what data leaves the
  machine is not recorded here.
- Copilot cloud agent: an Agents secret for a private registry is readable
  by the agent, and the firewall does not cover setup steps. What stops
  exfiltration over an allowed registry domain?
- Agents SDK: network egress is per provider. Which hosted providers enforce
  deny-by-default egress?
