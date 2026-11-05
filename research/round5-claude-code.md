---
url: https://raw.githubusercontent.com/anthropics/claude-code/main/CHANGELOG.md, https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md, https://registry.npmjs.org/@anthropic-ai/claude-code, https://raw.githubusercontent.com/anthropics/claude-code/main/LICENSE.md, https://code.claude.com/docs/llms.txt, https://code.claude.com/docs/en/how-claude-code-works, https://code.claude.com/docs/en/tools-reference, https://code.claude.com/docs/en/memory, https://code.claude.com/docs/en/permission-modes, https://code.claude.com/docs/en/sandboxing, https://code.claude.com/docs/en/sandbox-environments, https://code.claude.com/docs/en/hooks, https://code.claude.com/docs/en/skills, https://code.claude.com/docs/en/plugins/mods/overview, https://code.claude.com/docs/en/output-styles, https://code.claude.com/docs/en/headless, https://code.claude.com/docs/en/sub-agents, https://code.claude.com/docs/en/agents, https://code.claude.com/docs/en/workflows, https://code.claude.com/docs/en/goal, https://code.claude.com/docs/en/advisor, https://code.claude.com/docs/en/agent-sdk/overview, https://code.claude.com/docs/en/agent-sdk/agent-loop, https://code.claude.com/docs/en/context-window, https://code.claude.com/docs/en/platforms, https://code.claude.com/docs/en/claude-code-on-the-web, https://code.claude.com/docs/en/legal-and-compliance, https://code.claude.com/docs/en/costs, https://code.claude.com/docs/en/claude-apps-gateway, https://code.claude.com/docs/en/self-hosted-environments, https://code.claude.com/docs/en/claude-projects, https://code.claude.com/docs/en/commands, https://code.claude.com/docs/en/llm-gateway-protocol, https://code.claude.com/docs/en/best-practices, https://claude.com/pricing, https://www.anthropic.com/engineering, https://www.anthropic.com/engineering/claude-code-auto-mode, https://www.anthropic.com/engineering/how-we-contain-claude, https://www.anthropic.com/engineering/managed-agents, https://www.anthropic.com/engineering/april-23-postmortem, https://web.archive.org/web/20250602202220/https://www.anthropic.com/engineering/claude-code-best-practices, https://www.anthropic.com/features/making-of-claude-code, https://claude.com/blog/building-agents-with-the-claude-agent-sdk, https://www.latent.space/p/claude-code, https://www.ycrootaccess.com/p/boris-cherny-building-claude-code, https://simonwillison.net/2026/Jul/21/cat-and-thariq/, https://www.lennysnewsletter.com/p/head-of-claude-code-what-happens, https://stationf.co/news/boris-cherny, https://cybersecuritynews.com/claude-code-source-code-leaked/amp/, https://thehuman2ai.pages.dev/product/radar/techcrunch-anthropic-cat-wu, https://blizine.vercel.app/claude-codes-product-lead-talks-usage-limits-transparency-and-the-lean-harness-1779791729986, https://onlinemarketing.de/cases/claude-code-anthropic-erzaehlt-making-of, https://www.36kr.com/p/3885510549041417, https://code.claude.com/docs/en/how-claude-code-works.md, https://code.claude.com/docs/en/agent-sdk/agent-loop.md, https://code.claude.com/docs/en/workflows.md
fetched: 2026-11-04
verified: 2026-11-04 (adversarial fact-check pass, see last section)
---

# Claude Code (Anthropic): harness profile, November 2026

**Tags.** [P] confirmed on the primary source: Anthropic's docs, changelog,
npm registry, engineering blog, or a transcript published by the host of the
talk or podcast, fetched by me on 2026-11-04. [P*] primary source, but the
quote came back through a page summariser; check the wording before a slide
uses it. [S] secondary source only (news, aggregators, a host's write-up that
paraphrases). [E] extracted from a source and not cross-checked. [R] refuted
or misquoted; recorded so nobody reuses it. [O] our own analysis, labelled.
Spoken quotes from Latent Space, YC Root Access and Simon Willison's page are
from the host's own published transcript (Willison's is "an edited copy");
transcription errors in them are flagged where they matter. Dates are given
for every source. Anything dated before 2026-05-04 is marked **(older than 6
months)**.

Scope note: round 2 (`round2-agent-permission-models.md`) already covers
Claude Code's permission modes, settings precedence and secrets handling. This
file adds the harness architecture, tools, context, extensibility, philosophy
and the last six months of releases, plus new safety material (auto mode miss
rates, containment incidents) that answers one of round 2's open questions.

## Short version

- **What it is.** A closed-source agent harness for Claude models only. One
  engine runs behind the CLI, VS Code and JetBrains extensions, the desktop
  app's Code tab, claude.ai/code (cloud VMs), mobile, Slack/Claude Tag, GitHub
  Actions and the Agent SDK. Latest version 2.1.318 (2026-11-03); 561 npm
  releases since 2025-02-24. [P]
- **Loop.** A single model-driven loop: the model calls tools until it
  returns a reply with no tool calls. Everything else (subagents, plan mode,
  `/goal`, agent teams, dynamic workflows, agent view) is layered on that
  loop. Docs call this layer "the agentic harness". [P]
- **Tools are being removed, not added.** Glob and Grep left the default tool
  set on macOS/Linux in April 2026 (search goes through Bash with embedded
  `bfs`/`ugrep`); TodoWrite and the Task list tools were turned off for Opus
  4.8, Sonnet 5, Fable 5 and newer in August 2026; `/ultraplan` was removed.
  Cat Wu (Jul 2026) said the Edit tool exists mainly so the UI can render
  diffs and "we could probably just remove file edit and be totally fine". [P]
- **Context.** CLAUDE.md files (AGENTS.md read natively only since
  2026-09-18), `.claude/rules/`, auto memory (`MEMORY.md`, first 200 lines or
  25KB), summarise-style compaction, plus idle compaction (Oct 2026). No
  embeddings index: the team rejected RAG in 2025 for agentic search. [P]
- **Safety.** Auto mode (classifier-reviewed actions) became the starting
  mode for interactive sessions on every plan on 2026-09-28. Anthropic
  publishes its miss rate: 17% false negatives on real overeager actions
  (March 2026). OS sandbox (Seatbelt, bubblewrap) is off by default and does
  not run on native Windows. [P]
- **Extensibility.** MCP, skills (Agent Skills standard), 33 hook events with
  five handler types, plugins and marketplaces, subagents, output styles,
  headless `-p`, Agent SDK (Python/TS), and since 2026-10-01 **mods**:
  in-process JavaScript plugins that can redraw the UI and approve tool
  calls. No ACP support in docs or changelog. [P]
- **Philosophy.** "Do the simple thing first" (Boris Cherny, May 2025); "all
  the secret sauce, it's all in the model. And this is the thinnest possible
  wrapper over the model" (May 2025); build what works "20 or 30 percent of
  the time now" so the next model makes it work (Ben Mann, ~~Feb 2026~~ [R]
  published about July 2026, interviews recorded Feb to May 2026); delete
  the system prompt and re-add it line by line for each new model (Cherny,
  Jul 2026). [P]
- **Direction (last 6 months).** Many agents at once (agent view, dynamic
  workflows running "tens to hundreds of agents", Projects, cross-session
  messaging), cloud and self-hosted execution, enterprise plumbing (Claude
  apps gateway, self-hosted runners), proactivity (Claude Tag, "You should
  know" side agent), and a leaner prompt per model. [P]
- **For a bank** [O]: the harness changes several times a week (~~190~~ [R]
  165 published releases between May 4 and Nov 3, 2026, per the npm registry), defaults have flipped and flipped back
  within weeks, and Anthropic's own red team got a phished Claude Code session
  to exfiltrate `~/.aws/credentials` 24 times out of 25. Pin versions and rely
  on environment containment, not on the model or classifier.

---

## 1. What it is

| Item | Fact | Tag / source |
|---|---|---|
| Maker | Anthropic PBC | [P] LICENSE.md |
| License | Proprietary. "© Anthropic PBC. All rights reserved. Use is subject to Anthropic's Commercial Terms of Service." The GitHub repo `anthropics/claude-code` holds the changelog, issues and plugins, not the source. | [P] https://raw.githubusercontent.com/anthropics/claude-code/main/LICENSE.md |
| Embedding it in products | "preinstalling or running Claude Code in your products or services (e.g. in hosted sandboxes or other agent infrastructure) requires agreeing to our Commercial Terms of Service" | [P] https://code.claude.com/docs/en/legal-and-compliance |
| Agent SDK auth limit | "Anthropic does not allow third party developers to offer claude.ai login or rate limits for their products, including agents built on the Claude Agent SDK" | [P] https://code.claude.com/docs/en/agent-sdk/overview |
| First public release | npm 0.2.6 on 2025-02-24 (research preview alongside Claude 3.7 Sonnet) **(older than 6 months)** | [P] npm registry |
| 1.0 | 2025-05-22 | [P] npm registry |
| 2.0 | 2025-09-29: native VS Code extension, `/rewind`, "The Claude Code SDK is now the Claude Agent SDK" | [P] CHANGELOG 2.0.0 |
| Current | 2.1.318, published 2026-11-03; `stable` tag is 2.1.311 | [P] npm registry |
| Release cadence | 561 versions ever published (npm `time` entries; 557 still listed in `versions`, since 0.2.6 and 2.1.88 among others are unpublished); ~~190~~ **165** published releases from 2.1.128 (2026-05-04) to 2.1.318 (2026-11-03) inclusive. The version numbers span 191, but many numbers were skipped. | [P] npm registry, recounted 2026-11-04; [R] for the 190 figure |
| Runtime | Built on Bun; bundled Bun upgraded to 1.4 on 2026-06-17 (2.1.181). Willison notes Anthropic "started shipping Claude Code on Bun-in-Rust to everyone on June 17th" | [P] changelog; [S] Willison aside |
| Source leak | Version 2.1.88 (published 2026-03-30T22:36Z) is absent from the npm `versions` list and from the changelog, which jumps 2.1.87 to 2.1.89. News reports say a source map in that build exposed the TypeScript source on 2026-03-31. No Anthropic statement found. | [P] npm registry and changelog gap; [S] cybersecuritynews.com |

**Pricing** (claude.com/pricing, fetched 2026-11-04) [P*]: Free $0 (no Claude
Code); Pro $20/month ($17 annual); Max $100; Ultra $200; Team standard seat
$25 ($20 annual), premium seat $125 ($100 annual); Enterprise "US$20/seat/month,
billed annually, 20 seat minimum" with usage billed at API rates. API-key
use is billed per token. Docs give an enterprise average of "around \$13 per
developer per active day and \$150-250 per developer per month, with costs
remaining below \$30 per active day for 90% of users" [P]
https://code.claude.com/docs/en/costs.

**Surfaces** [P] (https://code.claude.com/docs/en/platforms,
https://code.claude.com/docs/en/how-claude-code-works):

| Surface | Notes | Launched |
|---|---|---|
| CLI | "the most complete surface"; scripting and Agent SDK are CLI-based | Feb 2025 |
| VS Code extension | native extension | 2.0.0, 2025-09-29 |
| JetBrains | runs the CLI in the IDE terminal | |
| Desktop app (Code tab) | parallel sessions with worktrees, diff view, app preview, computer use, Dispatch from phone; Linux beta, WSL support | 2.0.51, 2025-11-24 |
| Web / cloud (claude.ai/code) | Anthropic-managed VMs or self-hosted runners; `--cloud` and `--teleport` move sessions | Web-to-CLI teleport in 2.0.24, 2025-10-20 |
| Mobile | cloud sessions, Remote Control of local sessions | |
| Remote Control | drive a local session from browser or phone | changelog mentions from 2026-02 |
| Slack | "Claude Code in Slack" (per-user, Pro/Max/Ultra) and **Claude Tag** (org identity, Team/Enterprise, "multiplayer by default") | Tag launched about early July 2026 per Cat Wu [P, Willison transcript] |
| CI | GitHub Actions, GitLab CI/CD, Code Review (managed PR review, Team/Enterprise) | |
| Agent SDK | Python and TypeScript; "A library that runs the Claude Code binary" | renamed 2025-09-29 |
| Model providers | Anthropic API, Amazon Bedrock, Google Cloud's Agent Platform (Vertex), Microsoft Foundry, Claude Platform on AWS, LLM gateways, Anthropic's self-hosted **Claude apps gateway** | |

**Adoption numbers.** Only secondary or self-reported figures found:
- Lenny's Newsletter episode page (2026-02-19) says Claude Code grew "from a
  quick hack to 4% of public GitHub commits, with daily active users doubling
  last month" [S] (host's episode blurb, not Anthropic data)
  https://www.lennysnewsletter.com/p/head-of-claude-code-what-happens
- Cat Wu, July 2026: "our internal version of Claude Tag lands 65% of our
  product PRs right now" (Claude Code product engineering team only) [P,
  Willison edited transcript] https://simonwillison.net/2026/Jul/21/cat-and-thariq/
- No primary revenue or user count found. [O]

## 2. Agent loop architecture

**Single loop.** "When you give Claude a task, it works through three phases:
**gather context**, **take action**, and **verify results**. These phases
blend together." "Claude Code is the layer around the model that provides the
tools and manages the context the model sees. This surrounding layer is what
the term agentic harness refers to." [P]
https://code.claude.com/docs/en/how-claude-code-works

**When it stops.** SDK docs: "Claude continues calling tools and processing
results until it produces a response with no tool calls." [P]
https://code.claude.com/docs/en/agent-sdk/agent-loop. Extra stopping
controls layered on top [P]:
- `maxTurns` and budget limits in the SDK.
- `Stop` / `SubagentStop` hooks can block the stop; `type: "prompt"` and
  `type: "agent"` hooks can have a model or a subagent verify before
  stopping.
- `/goal` (2.1.139, 2026-05-11): "After each turn, a model checks whether the
  condition holds. If the model judges it not yet met, Claude starts another
  turn instead of returning control to you." https://code.claude.com/docs/en/goal
- Advisor tool (experimental, Anthropic API only): Claude consults a stronger
  model "before committing to an approach, when stuck on a recurring error, or
  before declaring a task complete". https://code.claude.com/docs/en/advisor

**Parallel tool calls.** "Read-only tools (like `Read`, `Glob`, `Grep`, and MCP
tools marked as read-only) can run concurrently. Tools that modify state (like
`Edit`, `Write`, and `Bash`) run sequentially." [P] agent-loop doc.

**Steering mid-turn.** A message typed while Claude works is queued and read
"as soon as those calls finish, within the same turn". [P]

**Ways to run more than one agent** (https://code.claude.com/docs/en/agents) [P]:

| Mechanism | Who holds the plan | Status (Nov 2026) |
|---|---|---|
| Subagents (`Agent` tool, formerly `Task`) | Claude, turn by turn; subagent gets its own context, returns a summary | GA; run in the background by default; built-ins `Explore`, `Plan`, `general-purpose`; forks inherit the parent conversation |
| Agent view (`claude agents`) | You dispatch and monitor background sessions | Research preview, 2.1.139, 2026-05-11 |
| Agent teams | A lead agent with teammates, shared task list, messaging | "Experimental and disabled by default"; first shipped 2.1.32, 2026-02-05 |
| Dynamic workflows (`Workflow` tool, `/workflows`) | "A script the runtime executes"; "Dozens to hundreds of agents per run" | 2.1.154, 2026-05-28 |
| Projects | One conversation spawning parallel cloud threads | Public beta, Pro/Max/Ultra only |
| `/batch` skill | Splits a change into 5 to 30 worktree-isolated subagents | |

Workflows doc: "With subagents, skills, and agent teams, Claude is the
orchestrator ... A workflow script holds the loop, the branching, and the
intermediate results itself, so Claude's context holds only the final
answer." [P] https://code.claude.com/docs/en/workflows. Cherny (Jul 2026):
"We use Bun as a sandbox and we start a virtual machine within Bun. And we
let Claude start a lot of agents and orchestrate them"; he described a
Zig-to-Rust rewrite of Bun as one dynamic workflow that "ran for 11 days".
[P, YC transcript] https://www.ycrootaccess.com/p/boris-cherny-building-claude-code

**Plan mode.** Claude "reads files, runs shell commands to explore, and writes
a plan, but does not edit your source"; with auto mode available, the
classifier reviews planning shell commands by default
(`useAutoModeDuringPlan`). `/ultraplan` (cloud plan review) is listed as
"Removed. Use plan mode instead." [P] permission-modes, commands docs.

**Background work.** Background Bash, the `Monitor` tool (2.1.98,
2026-04-09; streams a command's output lines back as events), `/loop` and
cron tools (2.1.71, 2026-03-06), cloud scheduled tasks (formerly
"routines"), `PushNotification`. [P]

**Verification as the core skill.** Cherny: "The verification is probably the
single most important thing that people do not get right, largely." [P, YC
transcript, 2026-07-27]

## 3. Tools

Full built-in list (tools reference, fetched 2026-11-04) [P]
https://code.claude.com/docs/en/tools-reference:

- **Files:** `Read` (text, images, PDFs by page range, notebooks; 25,000-token
  default page; `allow_large` since 2.1.296), `Write`, `Edit`,
  `NotebookEdit`.
- **Search:** `Glob`, `Grep` (ripgrep-based), `LSP` (needs code intelligence
  plugins), `ToolSearch` (deferred MCP tools).
- **Execution:** `Bash`, `PowerShell` (Windows), `Monitor`.
- **Web:** `WebFetch`, `WebSearch`; Claude in Chrome (GA 2026-07-01) and CLI
  computer use on macOS are integrations.
- **Orchestration:** `Agent`, `SendMessage`, `ListAgents`, `TaskStop`,
  `Workflow`, `Skill`, `AskUserQuestion`, `EnterPlanMode`/`ExitPlanMode`,
  `EnterWorktree`/`ExitWorktree`, `CronCreate/Delete/List`,
  `ScheduleWakeup`, `RemoteTrigger`, `SubagentHandback`.
- **Task tracking:** `TaskCreate/Get/List/Update`, `TodoWrite`, only on
  older models by default (see below).
- **Output/other:** `Artifact` (publish HTML/Markdown to claude.ai),
  `SendUserFile`, `PushNotification`, `ReportFindings`, `SendFeedback`,
  `ShareOnboardingGuide`, `EndConversation`, MCP resource tools,
  `WaitForMcpServers`.

**Edit format: exact string replacement.** "The Edit tool performs exact string
replacement. It takes an `old_string` and a `new_string` ... It doesn't use
regex or fuzzy matching." Checks: read-before-edit (always required for
"Claude Opus 4.6, Claude Haiku 4.5, and older models"; newer models can edit
an unread file when reading it would not prompt), exact match, uniqueness or
`replace_all: true`. A file that changed on disk can still be edited if
`old_string` matches current content exactly. [P] tools reference.

History of the edit format [P]: Dawn Drain (Anthropic research engineer), in
Anthropic's "The making of Claude Code" (~~2026-02-23~~ [R]: the page says
"Interviews were recorded in February–May 2026", so it cannot predate May;
two news reports dated 2026-07-07 say it went live that day [S for the exact
day]): "I spent an embarrassingly long time trying to teach Claude to write
diffs, because that seemed like the most natural way to express an edit in
text." ~~**(older than 6 months)**~~ (within the 6-month window)
https://www.anthropic.com/features/making-of-claude-code

Why a dedicated Edit tool still exists, Cat Wu (Jul 2026) [P, Willison edited
transcript]: "For file edit, the reason we have it is actually because we can
render it. ... The reason we had a dedicated file edit tool was so that we
could deterministically know that Claude was making a file change, so we could
show people this nice UI. A lot of new users onboarding still really like this
experience, so we've kept it around. But for a lot of us who are on auto mode
right now ... I don't think it actually matters, and we could probably just
remove file edit and be totally fine."

**Code search: agentic, via the shell.** Since 2.1.117 (2026-04-21) on native
macOS/Linux builds: "the `Glob` and `Grep` tools are replaced by embedded `bfs`
and `ugrep` available through the Bash tool — faster searches without a
separate tool round-trip (Windows and npm-installed builds unchanged)" [P]
changelog. The docs now say Glob and Grep are "Absent by default on macOS,
Linux, and WSL" and searches "reach your hooks and permission rules as `Bash`
calls" [P]. Thariq Shihipar: "we removed our grep and other search tools — glob
tools — in favor of native bash" [P, Willison transcript].
- [O] Consequence for policy writers: a `Grep(...)` permission rule or hook
  matcher does nothing on Linux/macOS by default; search must be governed as
  Bash.

**No embeddings index.** Cherny (Latent Space, 2025-05-07) **(older than 6
months)** [P, host transcript] https://www.latent.space/p/claude-code:
"very, very early versions of Claude actually used RAG. So we, like, indexed
the code base, and I think we were just using Voyage ... And eventually, we
landed on just agentic search as the way to do stuff. And there were two big
reasons, maybe three big reasons. So one is it outperformed everything. By a
lot." Asked which benchmark: "This was just vibes, so internal vibes. There's
some internal benchmarks also, but mostly vibes." On the index: "the code
drifts out of sync. And then there's security issues because this index has to
live somewhere. And then, you know, what if that provider gets hacked?"
- LSP is opt-in through code intelligence plugins [P]. A secondary report of a
  May 2026 Ars Technica interview says Cat Wu's team found no measurable gain
  from semantic-navigation plugins, so they stayed optional [S] (Ars could not
  be fetched).

**Task list tools turned off for new models.** 2.1.233 (2026-08-14):
"Todo/task-tracking tools (TaskCreate/Get/Update/List, TodoWrite) are no
longer available on Opus 4.8, Sonnet 5, Fable 5, Mythos 5, and newer models".
Docs give the reason: "On newer models, Claude keeps track of multi-step work
without a written checklist, and the tools' definitions and reminders take up
context." Cloud and background sessions keep them. [P] Verification note: the
rule was narrowed again in 2.1.268 (2026-09-10): the tools are now "offered
only on Claude 3.x, Opus 4.0–4.7, Sonnet 4.0–4.6, Haiku 4.5", so Haiku 5.5,
Opus 5.x and unrecognised gateway model IDs also lack them. The docs say "The
default set described here applies in Claude Code v2.1.268 and later." [P]
changelog 2.1.268, tools reference.

**Tool count philosophy.** Thariq: "overall we've been trying to trend towards
fewer tools." Cat Wu: "we try to keep the cardinality pretty low and make sure
that every tool we add has a distinct function from every other tool" [P,
Willison transcript, Jul 2026].

## 4. Context

**What loads at start** [P] how-claude-code-works, memory docs:
- System prompt. Per-model: "The lean system prompt is now the default for all
  models except Haiku, Sonnet, and Opus 4.7 and earlier" (2.1.154,
  2026-05-28); unknown model names on Bedrock/Vertex/Foundry get the shorter
  prompt (2.1.312, 2026-10-27). The "80% removed" figure is covered in
  `track2-thin-harness-evidence.md`.
- CLAUDE.md files: managed (org), user `~/.claude/CLAUDE.md`, project,
  `CLAUDE.local.md`; subdirectory files load lazily when Claude reads files
  there. Whole file loaded up to 4 MiB.
- **AGENTS.md:** read natively only since 2.1.277 (2026-09-18), and only when
  no CLAUDE.md exists in the working directory or above. `AGENTS.override.md`
  and `.agents/` are not read. [P]
- `.claude/rules/*.md` with optional `paths:` globs (since 2.0.64,
  2025-12-10).
- Auto memory: four note types (`user`, `feedback`, `project`, `reference`)
  under `~/.claude/projects/<project>/memory/`; "The first 200 lines of
  `MEMORY.md`, or the first 25KB, whichever comes first, are loaded";
  "Claude skips anything it can derive from the codebase". On by default since
  2.1.59 (2026-02-25). [P]
- Skill descriptions (bodies load on use), subagent descriptions (warning past
  15,000 tokens), MCP tool names only (definitions deferred via tool search),
  git status snapshot, system reminders (CLAUDE.md, output style, file-changed
  notes, attribution lines).

**Compaction** [P]:
- Summarise-style: "it compacts the conversation into a summary. The summary
  keeps your requests and key code snippets, but detailed instructions from
  early in the conversation may be lost." Control with a "Compact Instructions"
  section in CLAUDE.md or `/compact focus on ...`. Stops after repeated
  thrashing instead of looping.
- After compaction Claude Code "re-reads up to five of the files Claude has read
  or edited", re-injects skill bodies (truncated), and reloads startup content;
  path-scoped rules are summarised away. https://code.claude.com/docs/en/context-window
- Idle compaction (2.1.299, 2026-10-14; desktop and VS Code in 2.1.314): "a
  200K+ token conversation left idle for about 54 minutes is compacted before
  its one-hour prompt cache expires".
- Origin, Cherny 2025 **(older than 6 months)** [P, Latent Space]: "We tried a
  bunch of different options for compacting, you know, like rewriting old tool
  calls and truncating old messages and not new messages. And then in the end,
  we actually just did the simplest thing, which is ask Claude to summarize the,
  you know, the previous messages and just return that and that's it."

**Sessions.** Plaintext JSONL under `~/.claude/projects/`; resume, fork,
`/rewind` checkpoints (file snapshots before each edit, separate from git; do
not cover remote side effects). Since 2.1.300 transcripts record each
request's system prompt, tools and parameters. [P]

**Prompt-cache engineering is a recurring theme** [O, from changelog]: dozens
of 2026 entries fix cache breaks; the April 2026 quality postmortem traced one
of three regressions to a cache optimisation (see §8).

## 5. Safety

Round 2 covers modes, rules and admin lock-down. New or changed since then:

**Permission modes (Nov 2026)** [P] https://code.claude.com/docs/en/permission-modes:
`default` (shown as "Manual"), `acceptEdits`, `plan`, `auto`, `dontAsk`,
`bypassPermissions`. Deny rules apply in every mode. Protected paths and
"critical-path" `rm` removals are never auto-approved.

**Auto mode timeline** [P] changelog:
- Engineering post 2026-03-25; available to Max on Opus 4.7 in 2.1.111
  (2026-04-16); on Bedrock/Vertex/Foundry with opt-in 2.1.158 (2026-05-30),
  without opt-in 2.1.207 (2026-07-10).
- Starting mode for interactive sessions on third-party providers 2.1.283
  (2026-09-25), on "every plan and provider" 2.1.284 (2026-09-28). [P]
  Verification note: the permission-modes doc now pins the whole change to
  "v2.1.283 or later", while the changelog splits it across 2.1.283 and
  2.1.284; the changelog is the more precise record. Exceptions in the docs:
  orgs with the HIPAA configuration start in `default` (v2.1.285+), and on an
  unsupported model the session "starts in Manual instead".
- Headless flip-flop: 2.1.285 (2026-09-29) made `claude -p` and the Python SDK
  on third-party providers start in auto mode; 2.1.302 (2026-10-16) reverted
  that: "`claude -p` and Agent SDK sessions with no permission mode ... start
  in `default` mode". [P]

**How auto mode works** (Mar 2026, **older than 6 months**, author John
Hughes) [P] https://www.anthropic.com/engineering/claude-code-auto-mode:
- Input layer: a server-side prompt-injection probe scans tool outputs and adds
  a warning. Output layer: a transcript classifier (then Sonnet 4.6; default
  is now Sonnet 5 per docs) in two stages: a single-token filter told to "err
  on the side of blocking", then chain-of-thought only on flagged actions.
- "The classifier sees only user messages and the agent's tool calls; we strip
  out Claude's own messages and tool outputs, making it reasoning-blind by
  design." Reason: "we want it to judge what the agent did, not what the agent
  said."
- Tiers: built-in safe-tool allowlist and user rules; in-project file edits
  allowed without a classifier call; everything else to the classifier. On
  entering auto mode, broad rules such as `Bash(*)`, wildcarded interpreters
  and package-manager run commands are dropped.
- Default trust boundary: "the only thing the classifier trusts is the git repo
  you're currently working in." More than twenty default block rules.
- **Measured results** (answers round 2's open question on miss rates):

| Dataset | Stage 1 | Full pipeline |
|---|---|---|
| Real internal traffic, n=10,000 (false positive rate) | 8.5% | 0.4% |
| Real overeager actions, n=52 (false negative rate) | 6.6% | **17%** |
| Synthetic exfiltration, n=1,000 (false negative rate) | 1.8% | 5.7% |

- "The 17% false-negative rate on real overeager actions is the honest number."
  "If you are manually approving every action carefully, it's arguably a
  regression ... It is not a drop-in replacement for careful human review on
  high-stakes infrastructure." The baseline: "in practice users accept 93% of
  them anyway" (manual prompts).
- [O] Caveats for slides: n=52 is small; the classifier model has changed
  since (Sonnet 4.6 then, Sonnet 5 now, or server-side review); no newer
  numbers published.

**Server-side review (since about 2.1.271, Sep 2026).** Claude Code can ask the
API server to review actions inside the model request; if the server gives no
verdict, "Claude Code denies the action rather than run it unreviewed". [P]

**Sandboxing** [P] https://code.claude.com/docs/en/sandboxing:
- Seatbelt on macOS, bubblewrap (+ socat) on Linux and WSL2, built on the
  open-source `@anthropic-ai/sandbox-runtime`. "On native Windows, Claude Code
  runs commands unsandboxed."
- "The sandbox is off by default." It wraps Bash, PowerShell and Monitor
  commands only; "Claude's file tools, MCP servers, and hooks run outside it".
  Reads default to "Most of the machine, including credential files such as
  `~/.ssh` and `~/.aws/credentials`" unless denied. Network goes through a local
  proxy with allowed domains "which start empty".
- Credential `mask` mode (2.1.221, 2026-08-03, Linux/WSL): sandboxed commands
  see a sentinel; the proxy substitutes the real value on egress.
- Containment post: the sandbox gave "an 84% reduction in permission prompts".
- Cloud sessions: "each session runs in an isolated, Anthropic-managed VM";
  git credentials stay outside the sandbox behind a proxy. Self-hosted runners
  (public beta, Team/Enterprise) move isolation to the customer.
- New org locks: `permissions.blockReadsOutsideWorkingDirectories` (2.1.257)
  and `permissions.blockWritesOutsideWorkingDirectories` (2.1.314,
  2026-10-30). [P]

**Incidents Anthropic has disclosed** ("How we contain Claude across products",
2026-05-25) [P] https://www.anthropic.com/engineering/how-we-contain-claude:
- Pre-trust execution: "Between mid-2025 and January 2026" three reported
  vulnerabilities ran code before the folder-trust prompt, e.g. a hook in a
  cloned repo's `.claude/settings.json`. Fix: defer project config until
  trust is accepted.
- Phishing red team (Feb 2026): an employee was phished into launching Claude
  Code with a prompt that asked it to read `~/.aws/credentials` and POST it out.
  "Across 25 retries of that prompt, Claude completed the exfiltration 24
  times." "The only defense that holds in this situation is the environment."
- Models "'helpfully' escape a sandbox in order to complete a task".
- Principle: "Design for containment at the environment layer first, then steer
  behavior at the model layer." "Match isolation strength to the user's capacity
  for oversight."
- Contrast with Cowork: Claude Code has "a privileged process [that] sits
  outside the sandbox deciding per-command whether to enforce it; a persuasive
  injected prompt or a fatigued approval click can get that process to run
  something un-sandboxed".
- Stated next risks: persistent memory poisoning (CLAUDE.md, memory), multi-agent
  trust escalation, agent identity.

**A vendor claim to handle carefully.** Cherny (YC, 2026-07-27): with an aligned
model, a prompt-injection classifier "which we run for all traffic", and the auto
mode classifier, "with these three layers, we just cannot demonstrate prompt
injection anymore." [P, YC transcript; the transcript renders Fable as "Table"
and Chris Olah as "Crysola"]. [O] This sits beside the same company's 24/25
phishing result two months earlier, where the instruction came through the user.
Do not quote one without the other.

## 6. Extensibility

| Mechanism | What it is | Since | Tag |
|---|---|---|---|
| MCP | stdio/HTTP servers; tool definitions deferred and found by `ToolSearch` (auto since 2.1.7, 2026-01-13, when MCP tools exceed 10% of context) | 2024-25 | [P] |
| Hooks | 33 events (SessionStart, PreToolUse, PermissionRequest, PermissionDenied, PostToolBatch, Stop, PreCompact, InstructionsLoaded, FileChanged, PreModelSwitch, ...); five handler types: `command`, `http`, `mcp_tool`, `prompt`, `agent` (experimental); `onFailure: "block"` (2.1.295) lets a failing hook fail closed | 1.0.38, 2025-06-30 | [P] |
| Skills | `SKILL.md`, "follow the Agent Skills open standard" (agentskills.io) plus Claude Code extensions; descriptions load at start, bodies on use; bundled skills like `/code-review`, `/batch`, `/debug` | 2.0.20, 2025-10-16 | [P] |
| Plugins + marketplaces | bundle skills, agents, hooks, MCP servers, mods | 2.0.12, 2025-10-09 | [P] |
| **Mods** | "A mod is a plugin that changes how Claude Code looks and behaves. It's made of JavaScript or TypeScript event handlers" that can draw panes, redraw Claude Code's own UI, "hold a tool call", "send one request to a different model", and approve tool calls. "Mods aren't sandboxed." Some built-in features (`/diff`, "You should know") are mods | 2.1.287, 2026-10-01 ("Added Claude Mods: plugins may now modify deeper behavior") | [P] |
| Subagents | Markdown with frontmatter (`tools`, `model`, `permissionMode`, `memory`, `isolation: worktree`, `autoCompactWindow`, `maxTurns`) | 1.0.6x, Jul 2025 | [P] |
| Output styles | Default, Proactive, Concise, Explanatory, Learning, or custom; they modify the system prompt | 1.0.81, 2025-08-14 | [P] |
| Headless | `claude -p`, `--output-format json/stream-json`, `--json-schema`, `--bare` (skips hooks, skills, plugins, MCP, CLAUDE.md "for CI and scripts where you need the same result on every machine") | early 2025; `--bare` 2.1.81, 2026-03-20 | [P] |
| Agent SDK | Python and TS; bundles the native binary; same tools, hooks, permissions, sessions, skills, plugins | renamed 2025-09-29 | [P] |
| Managed Agents | Anthropic-hosted harness on the Claude Platform; session log, harness and sandbox as separate interfaces; self-hosted sandboxes supported | eng. post 2026-04-08 | [P] |
| Channels | push events (Telegram, Discord, your server) into a running local session | 2026 | [P] |
| ACP (Agent Client Protocol) | Not mentioned anywhere in the docs index or changelog | | [P] absence |

Managed Agents design statement (2026-04-08, **older than 6 months**) [P]
https://www.anthropic.com/engineering/managed-agents: "harnesses encode
assumptions about what Claude can't do on its own. However, those assumptions
need to be frequently questioned because they can go stale as models improve."
"We're opinionated about the shape of these interfaces, not about what runs
behind them." Example: context resets added for Sonnet 4.5's "context anxiety"
"had become dead weight" on Opus 4.5.

## 7. Model coupling

- Claude models only, through Anthropic or the clouds that host Claude. The
  docs describe Claude Code as using "Claude models"; the gateway guide covers
  routing Claude traffic, not other vendors. [P] [O]: pointing
  `ANTHROPIC_BASE_URL` at a non-Claude model behind an Anthropic-format proxy
  is unsupported; behaviour falls back to defaults for unknown model names
  (shorter prompt, no task tools, adaptive thinking sent).
- Behaviour is tuned per model inside the harness [P]: lean vs full system
  prompt; read-before-edit enforced only for older models; task tools only
  on older models; auto mode only on Opus 4.6+/Sonnet 4.6+/Haiku 5.5/Fable on
  the Anthropic API, Sonnet 5+/Opus 4.7+ on clouds; Explore subagent runs on
  Opus when the main model is Fable.
- Models added in the window: Fable 5 (2026-06-09), Sonnet 5 (2026-06-30, made
  the default), Opus 5 (2026-07-24), Fable 5.1 (2026-09-01), Opus 5.5
  (2026-09-22, default Opus, $4/$20 per Mtok), Sonnet 5.5 (2026-09-28), Haiku
  5.5 (2026-10-07). [P] changelog
- Does Anthropic train for its own harness? No primary source found that says
  models are trained on Claude Code's specific tools. Cherny says capability is
  taught in training ("some subset of the things, the model does learn") and
  that Claude Code is where Anthropic observes models; Station F reports him
  saying "For us, the model is the product and the product is the model" [S,
  host write-up, 2026-03-13] https://stationf.co/news/boris-cherny. [O] Coupling
  is tight in both directions: one vendor's models, and a harness re-tuned for
  each release.

## 8. Philosophy (from the builders' own words)

**Do the simple thing first.** Boris Cherny, Latent Space, 2025-05-07 **(older
than 6 months)** [P, host transcript] https://www.latent.space/p/claude-code:
- "Generally, at Anthropic, we have this product principle of do the simple
  thing first. And I think that the way we build product is really based on
  that principle. So you kind of staff things as little as you can and keep
  things as scrappy as you can because the constraints are actually pretty
  helpful."
- On CLAUDE.md: "We had all these crazy ideas about like memory architectures
  ... But in the end, the thing we did is ship the simplest thing, which is,
  you know, it's a file that has some stuff. And it's auto-read into context."
- "And it's funny when the model is so good, the simple thing usually works.
  You don't have to over-engineer it."

**Thin wrapper, secret sauce in the model.** Same episode [P]: "generally our
approach is, you know, all the secret sauce, it's all in the model. And this is
the thinnest possible wrapper over the model. We literally could not build
anything more minimal." And: "now, actually, I feel everything is the model.
Like, that's the thing that wins in the end. And it just, as the model gets
better, it subsumes everything else." (He was answering a question on knowledge
graphs for memory.)

**Low-level, unopinionated, Unix-like.** Anthropic engineering blog, 2025-04-18
**(older than 6 months)**: "Claude Code is intentionally low-level and
unopinionated, providing close to raw model access without forcing specific
workflows. This design philosophy creates a flexible, customizable, scriptable,
and safe power tool." [P via Wayback snapshot 2025-06-02]
https://web.archive.org/web/20250602202220/https://www.anthropic.com/engineering/claude-code-best-practices.
[R] Do not cite the live URL for this line: it now redirects (308) to
code.claude.com/docs/en/best-practices, which no longer contains it. Cherny,
2025: "It's raw access to the model"; Latent Space's own summary calls it "a
Unix utility" [P].

**Build for the model that is coming.**
- Cherny 2025 [P, Latent Space]: "We want to build something that's kind of
  much earlier on that curve and something that will maybe be a big product,
  you know, a year from now ... As the model improves. And that's why code runs
  in a terminal."
- Ben Mann ("Anthropic co-founder and Labs team lead" per the page), "The
  making of Claude Code", ~~2026-02-23 **(older than 6 months)**~~ [R] published
  about 2026-07-07, interviews recorded Feb to May 2026 [P, speaker and wording
  confirmed on the page]: "you have to build something that works 20 or
  30 percent of the time now, so that when the next model comes out, it works 80
  percent of the time."
- Lenny's Podcast (2026-02-19) is widely reported to include "bet on a model six
  months out" in Cherny's tips [S]; the transcript is paywalled and was not
  checked. https://www.lennysnewsletter.com/p/head-of-claude-code-what-happens

**Delete and re-derive for every model.** Cherny, YC Startup School, published
2026-07-27 [P, YC transcript] https://www.ycrootaccess.com/p/boris-cherny-building-claude-code:
- "Every time there's a new model, in research, we call this ablation. What this
  means is you delete the entire system prompt and then bring it back line by
  line to figure out the impact of each individual line."
- "We unship tools all the time. We delete code in the harness all the time. If
  you look at the code that's in the Claude Code harness today, almost all of it
  is about safety and permissions and static analysis. There's a bunch of UI
  code."
- To users: "every six months, delete your [CLAUDE.md], delete your skills,
  delete your hooks. See what the model does and it might surprise you." (The
  transcript renders CLAUDE.md as "quantum D".)
- "the model is actually a little bit more intelligent without these prompts.
  ... But when you use Claude Code as a product, you do actually want some of
  these prompts."
- Shipped counterpart: `/doctor prompt-audit` (2.1.283, 2026-09-25) "to audit
  your CLAUDE.md files, skills, agents and commands for prompting patterns
  written for older models". [P]

**Dogfooding with a retention bar.** Cat Wu, AI Engineer World's Fair, written up
2026-07-21 [P, Willison edited transcript]: "We have an internal bar for the
number of active users and the amount of retention a feature has to have before
we share it with the world. ... if the feature isn't polished, people will churn
— and then we shouldn't ship that feature." Cat Wu, 2025 [P, Latent Space]: "we
definitely still hold a very high bar for net new features."

**Small team on purpose.** Cherny, "The making of Claude Code" [P]: "keeping the
team small was actually very important to our success. It helped us be really
creative with resources, and kept us from overengineering. And it forced us to
use Claude more."

**Giving the model a computer.** "The key design principle behind Claude Code is
that Claude needs the same tools that programmers use every day." (Anthropic,
2025-09-29, **older than 6 months**) [P]
https://claude.com/blog/building-agents-with-the-claude-agent-sdk

**What they say they reject** [P unless marked]:

| Rejected | Who, when |
|---|---|
| RAG / embeddings index for code | Cherny, May 2025 (drift, security, worse results) |
| Elaborate memory architectures, knowledge graphs | Cherny, May 2025 |
| Rewriting or truncating old tool calls for compaction | Cherny, May 2025 ("simplest thing" won) |
| Big UI and scaffolding over the model (2025 position) | Cherny, May 2025 |
| Many overlapping tools | Thariq and Cat Wu, Jul 2026 |
| Examples and "don't do X" lists in system prompts for new models | Willison summary of Cat and Thariq, Jul 2026 [S, host summary]; see `track2-anthropic-new-rules-context-engineering.md` |
| Per-action human approval as the main safety control | Containment post, May 2026 ("we've found the approach to be fallible") |
| Lowering default effort to save latency | April 2026 postmortem: "This was the wrong tradeoff." |

**The harness can make the model look worse.** April 23, 2026 postmortem
**(older than 6 months)** [P] https://www.anthropic.com/engineering/april-23-postmortem:
three harness changes (default effort lowered to medium on Mar 4; a bug that
cleared prior thinking every turn after an idle hour, Mar 26; a verbosity line in
the system prompt, Apr 16) produced user reports of a dumber model. "The API was
not impacted." The thinking bug "made it past multiple human and automated code
reviews, as well as unit tests, end-to-end tests, automated verification, and
dogfooding." [O] This is the cleanest primary evidence available that harness
changes alone move perceived model quality.

## 9. Direction

**Shipped, May 4 to Nov 3, 2026** [P] changelog with npm dates:

| Date | Version | Change |
|---|---|---|
| 05-11 | 2.1.139 | Agent view (research preview); `/goal` |
| 05-28 | 2.1.154 | Dynamic workflows; lean system prompt default for newer models |
| 05-30 | 2.1.158 | Auto mode on Bedrock/Vertex/Foundry (opt-in) |
| 06-08 | 2.1.169 | `--safe-mode` (start with all customisations off) |
| 06-09 | 2.1.170 | Claude Fable 5 |
| 06-30 | 2.1.197 | Sonnet 5 default, native 1M context |
| 07-01 | 2.1.198 | Claude in Chrome GA |
| ~07 | | Claude Tag in Slack (per Cat Wu) [P, Willison] |
| 07-24 | 2.1.219 | Opus 5 |
| 08-03 | 2.1.221 | Sandbox credential masking |
| Aug | 2.1.228+ | Self-hosted runners; Claude apps gateway (SSO, per-IdP-group model access, spend limits, OTLP) |
| 08-14 | 2.1.233 | Task/Todo tools off for new models |
| 09-01 | 2.1.257 | Fable 5.1 |
| 09-18 | 2.1.277 | AGENTS.md read natively |
| 09-22 | 2.1.280 | Opus 5.5 default Opus |
| 09-25/28 | 2.1.283/284 | Auto mode is the starting mode everywhere; `/doctor prompt-audit` |
| 10-01 | 2.1.287 | Claude Mods; "You should know" side agent ("watches your back and flags things you or Claude might miss") |
| 10-07 | 2.1.293 | Haiku 5.5 |
| 10-08 | 2.1.295 | Hooks can fail closed (`onFailure: "block"`) |
| 10-14 | 2.1.299 | Idle compaction |
| 10-16 | 2.1.302 | Headless back to Manual default; notice that standalone Claude Design "closes by December 14, 2026" |
| 10-30 | 2.1.314 | `blockWritesOutsideWorkingDirectories` |
| 10-31 | 2.1.316 | Opus 4.8 fast mode deprecated, removal 2026-11-30 |

**Publicly stated next steps:**
- Auto mode: "We'll continue expanding the real overeagerness testset and
  iterating on improving the safety and cost of the feature." (Mar 2026) [P]
- Containment work items: memory-poisoning defences ("Good classifiers on
  session startup will need to become more commonplace"), multi-agent trust,
  agent identity (May 2026) [P].
- ~~Cherny (Jul 2026): "everyone in this room should be building something that
  runs hopefully multiple months and thousands of agents"~~ [R] misattributed
  and misquoted: in the YC transcript the host, Diana, says it while closing
  the session: "someone in this room should be building something that runs
  hopefully multiple months and thousands of agents now that you have the
  account to do it." What Cherny himself said: dynamic workflows "let you
  orchestrate dozens, hundreds, thousands of agents to do work productively"
  [P, YC transcript]. Cherny also says Opus 5 with auto mode "can go for days, weeks, months at a time. ...
  You don't even need to use scaffolding. So you don't need slash goal". [O] A
  claim about the model, stated by its vendor.
- Cat Wu (TechCrunch, 2026-05-13): the next phase is proactive AI that learns
  your workflow and sets up automations [S, aggregator summaries only]. Shipped
  items that match: Claude Tag's standing instructions, the Proactive output
  style, "You should know". [P for the shipped items]
- Claude Tag "as the evolution of Claude Code" (Cat Wu, Jul 2026) [P,
  Willison transcript].

## 10. Notes for the presentation [O]

- The best single slide on Claude Code's philosophy is the pair "thinnest
  possible wrapper" (2025) and "almost all of it is about safety and
  permissions and static analysis" (2026). The loop stayed thin; the code
  moved into safety, permissions and UI.
- For a Copilot-only bank, Claude Code matters as the design source: Copilot
  already reads CLAUDE.md, `.claude/skills/`, `.claude/settings.json` hooks
  (round 1). Claude Code is also an `engine:` option in GitHub Agentic
  Workflows (round 1, track1-other-surfaces).
- Policy writers should know: search runs as Bash on Linux/macOS; the sandbox
  is off by default and absent on native Windows; mods and hooks run outside
  the sandbox; auto mode misses about 1 in 6 overeager actions in Anthropic's
  own test set.

## Verification pass (2026-11-04)

Adversarial re-check against primary pages, fetched 2026-11-04 (raw page
text or the `.md` version of each docs page, grepped for exact wording; npm
registry JSON counted by script).

**Confirmed on the primary page [P]:**
1. Auto mode numbers: 0.4% FPR on n=10,000 real traffic, 17% FNR on n=52 real
   overeager actions, 5.7% on n=1,000 synthetic exfiltration; "The 17%
   false-negative rate on real overeager actions is the honest number"; "in
   practice users accept 93% of them anyway". Author John Hughes, Mar 25, 2026.
2. Containment post (May 25, 2026; McGuinness, Grace, De Jonghe, Eaton,
   Ribbink): Feb 2026 phish, "Across 25 retries of that prompt, Claude
   completed the exfiltration 24 times"; "The only defense that holds in this
   situation is the environment".
3. Same post: "an 84% reduction in permission prompts"; three pre-consent
   vulnerabilities reported mid-2025 to January 2026, example a hook in a
   cloned repo's `.claude/settings.json`.
4. Changelog 2.1.117 (npm 2026-04-21) Glob/Grep replaced by embedded `bfs` and
   `ugrep` on native macOS/Linux builds; docs now also list WSL.
5. Changelog 2.1.233 (npm 2026-08-14) and the docs' reason text. Added the
   2.1.268 narrowing (see §3).
6. Changelog 2.1.283/2.1.284 and permission-modes doc; sandbox "off by
   default"; "On native Windows, Claude Code runs commands unsandboxed."
7. Latent Space (2025-05-07): "secret sauce ... thinnest possible wrapper",
   "do the simple thing first", RAG/Voyage/"just vibes", "drifts out of sync",
   compaction "simplest thing", CLAUDE.md "crazy ideas", "everything is the
   model", "raw access to the model", Cat Wu "very high bar for net new
   features". All verbatim and correctly attributed.
8. YC Root Access (Jul 27, 2026): ablation passage, "almost all of it is about
   safety and permissions and static analysis", "quantum D" line, "a little
   bit more intelligent", Bun sandbox and "ran for 11 days", "single most
   important thing", "cannot demonstrate prompt injection anymore", "Table"
   and "Crysola" transcription errors.
9. Making-of page: Ben Mann quote, speaker label "Anthropic co-founder and
   Labs team lead"; Dawn Drain and Cherny small-team quotes also verbatim.
10. April 23 postmortem: three changes (Mar 4 effort high to medium, Mar 26
    thinking-clearing bug, Apr 16 verbosity line); "The API was not
    impacted."; "This was the wrong tradeoff."; "made it past multiple human
    and automated code reviews...".
11. Mods overview: "Mods aren't sandboxed."; redraw UI, hold a tool call, send
    a request to a different model, "approve a tool call before you're asked";
    changelog 2.1.287 (npm 2026-10-01) "Added Claude Mods".
12. Memory doc: AGENTS.md "requires Claude Code v2.1.277 or later" (npm
    2026-09-18), read "only when you have no `CLAUDE.md` in your working
    directory or above it"; `AGENTS.override.md` and `.agents/` not read; 4 MiB
    CLAUDE.md limit; MEMORY.md 200 lines / 25KB.

Other spot checks confirmed [P]: Willison page (Cat Wu Edit-tool quote, 65%
quote, "evolution of Claude Code", Thariq "removed our grep", "fewer tools",
"cardinality", retention bar, Bun-in-Rust aside); Managed Agents (Apr 8, 2026)
three quotes; Agent SDK blog (Sep 29, 2025) "same tools that programmers use
every day"; Wayback best-practices (Apr 18, 2025) "intentionally low-level and
unopinionated"; Station F (Mar 13, 2026) "the model is the product" [S as
labelled]; Lenny's blurb (Feb 19, 2026) "4% of public GitHub commits" [S as
labelled]; docs quotes for "agentic harness", agent-loop stop rule and
parallel read-only tools, workflows "Claude is the orchestrator" and "Dozens
to hundreds of agents per run"; costs doc $13/day, $150-250/month, <$30 for
90%; npm dates for 0.2.6, 1.0.0, 2.0.0, 2.1.88 (2026-03-30T22:36Z), latest
2.1.318 (2026-11-03), stable 2.1.311; direction-table entries for 2.1.139,
2.1.154, 2.1.169, 2.1.170, 2.1.198, 2.1.257, 2.1.280, 2.1.293, 2.1.299,
2.1.302, 2.1.314.

**Corrected [R]:**
- Release count May 4 to Nov 3, 2026: 190 is wrong; 165 published releases
  (the agent appears to have counted version numbers, which skip). Total of
  561 holds only as "ever published"; 557 are listed today.
- "The making of Claude Code" date: not 2026-02-23. The page itself says
  interviews were recorded February to May 2026; two news reports dated
  2026-07-07 say it went live that day. Removed its "older than 6 months"
  flags; the Ben Mann quote is from about July 2026, not Feb 2026.
- "everyone in this room should be building something that runs hopefully
  multiple months and thousands of agents" was said by the YC host Diana, not
  Cherny, and the word is "someone". Do not put it on a Cherny slide.

**Nuances added, not errors:** task tools narrowed again in 2.1.268; auto-mode
starting-mode exceptions (HIPAA orgs, unsupported models); docs and changelog
disagree on whether 2.1.283 or 2.1.284 made auto mode the default everywhere.

**Not verified:** claude.com/pricing tiers (left at [P*]); the exact
publication day of the making-of page (only secondary reports give
2026-07-07); hook event count (33) and handler types; the Ars Technica / Cat
Wu LSP report and TechCrunch Cat Wu piece (left at [S]); the Lenny's "six
months out" tip (paywalled, not on the free page); source-leak news (left at
[S]); model release dates for Sonnet 5, Opus 5, Sonnet 5.5 (not individually
re-checked).
