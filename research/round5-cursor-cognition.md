---
url: https://cursor.com/changelog, https://cursor.com/changelog/page/2, https://cursor.com/changelog/page/3, https://cursor.com/changelog/page/4, https://cursor.com/changelog/page/5, https://cursor.com/blog, https://cursor.com/blog/page/2, https://cursor.com/blog/joining-spacex, https://cursor.com/blog/self-driving-codebases, https://cursor.com/blog/composer, https://cursor.com/blog/composer-2, https://cursor.com/blog/composer-2-5, https://cursor.com/blog/self-summarization, https://cursor.com/blog/tab-rl, https://cursor.com/blog/instant-apply, https://cursor.com/en-US/blog/semsearch, https://cursor.com/blog/fast-regex-search, https://cursor.com/blog/improved-token-efficiency, https://cursor.com/blog/projects, https://cursor.com/blog/agent-sdk, https://cursor.com/blog/third-era, https://cursor.com/blog/cursor-3, https://cursor.com/blog/self-hosted-machines, https://cursor.com/blog/git-at-any-scale, https://cursor.com/blog/claude-code-extension-security-notice, https://cursor.com/compile, https://cursor.com/pricing, https://cursor.com/llms.txt, https://cursor.com/docs/models, https://cursor.com/docs/agent/overview, https://cursor.com/docs/agent/tools, https://cursor.com/docs/agent/plan-mode, https://cursor.com/docs/agent/security/run-modes, https://cursor.com/docs/context/rules, https://cursor.com/docs/context/semantic-search, https://cursor.com/docs/subagents, https://cursor.com/docs/hooks, https://cursor.com/docs/customize-cursor, https://cursor.com/docs/cli/overview, https://cursor.com/docs/cli/acp, https://cursor.com/docs/cli/reference/permissions, https://cursor.com/docs/bugbot, https://cursor.com/docs/cloud-agent, https://cursor.com/docs/agent-sdk/reference/tools, https://forum.cursor.com/t/what-do-you-think-about-cursor-removing-the-codebase-indexing-settings/165899, https://x.ai/news/grok-4-7, https://cognition.com/blog, https://cognition.com/blog/dont-build-multi-agents, https://cognition.com/blog/multi-agents-working, https://cognition.com/blog/what-we-learned-building-cloud-agents, https://cognition.com/blog/devin-for-terminal, https://cognition.com/blog/introducing-devin-desktop, https://cognition.com/blog/devin-fusion, https://cognition.com/blog/local-fusion, https://cognition.com/blog/making-fable-cheaper-than-opus, https://cognition.com/blog/swe-2, https://cognition.com/blog/swe-2-flash, https://cognition.com/blog/swe-1-7, https://cognition.com/blog/swe-grep, https://cognition.com/blog/one-year-of-building-together, https://cognition.com/blog/series-e, https://cognition.com/blog/1b-run-rate, https://cognition.com/blog/ai-guarantee, https://cognition.com/blog/introducing-devin-2-2, https://cognition.com/blog/devin-can-now-manage-devins, https://cognition.com/blog/testing-development, https://cognition.com/blog/devin-sonnet-4-5-lessons-and-challenges, https://cognition.com/blog/devin-in-windsurf, https://cognition.com/blog/devin-security, https://cognition.com/blog/corridor-joining-cognition, https://cognition.com/blog/practical-guide-to-security-november-2026, https://devin.ai/pricing, https://docs.devin.ai/llms.txt, https://docs.devin.ai/_llms/en/desktop.txt, https://docs.devin.ai/onboard-devin/environment.md, https://docs.devin.ai/onboard-devin/knowledge-onboarding.md, https://docs.devin.ai/work-with-devin/deepwiki.md, https://docs.devin.ai/desktop/devin-local/overview.md, https://docs.devin.ai/cli/index.md, https://docs.devin.ai/cli/sandbox.md, https://docs.devin.ai/cli/extensibility/rules.md, https://docs.devin.ai/cli/adaptive.md, https://venturebeat.com/technology/cursors-composer-2-was-secretly-built-on-a-chinese-ai-model-and-it-exposes-a, https://www.bnnbloomberg.ca/business/artificial-intelligence/2026/06/16/spacex-to-buy-ai-coding-startup-cursor-for-us60-billion-in-enterprise-push/, https://www.kucoin.com/news/flash/cursor-unveils-1-5-trillion-parameter-ai-model-and-git-platform-origin-at-compile-summit, https://theresanaiforthat.com/model/composer-3/, https://www.datalearner.com/en/ai-models/pretrained-models/composer-3, https://forum.cursor.com/t/165899.json
fetched: 2026-11-04
verified: 2026-11-04 (adversarial pass; see last section)
---

# Round 5: Cursor (Anysphere, now SpaceX) and Cognition (Devin, Devin Desktop, ex-Windsurf)

**Tags.** [P] confirmed on the vendor's or author's own page, fetched 2026-11-04. [P*] a quote from a primary page that came back through the WebFetch summariser; the page is right, but check exact wording against the live page before it goes on a slide. (Every page in this file was read through that summariser, so every quote is [P*] unless marked otherwise.) [S] secondary source only (news, aggregators, social posts reported by press). [E] extracted from one source and not cross-checked. [R] refuted or stale claim that is circulating; recorded so nobody reuses it. [O] our own analysis, clearly labelled. Anything dated before about May 2026 is flagged "(older than 6 months)".

**Verification pass, 2026-11-04.** A second agent re-fetched the cited pages as raw HTML (curl) and string-matched the quotes. A quote now tagged [P] matched the raw page text exactly (after decoding HTML entities and curly apostrophes). [P*] now means the wording was checked only through the WebFetch summariser. Corrections are marked "[R] ... -> correction" inline.

## Short version

- [P] **Cursor is now owned by SpaceX.** Cursor's own post of Aug 14, 2026 says it has "officially been acquired by SpaceX" and that this "completes the acquisition process that started in April" (https://cursor.com/blog/joining-spacex; the post gives no price). Plans were rebuilt around a shared Cursor + Grok usage pool; the $8 Plus tier gets Grok models only, third-party models need Premium ($30) or above (https://cursor.com/pricing).
- [P] **Cursor dropped its embeddings index.** Staff confirmed in July 2026 that "Semantic/embeddings indexing is being turned down in favor of grep-based retrieval"; the agent now uses a local "Instant Grep" index plus file reads ([R] "trigram" index -> Cursor's Mar 2026 post explains trigram indexes as background but says its design uses "sparse n-grams") (forum thread, docs page). This reverses Cursor's own Nov 2025 post that called semantic search "currently necessary." Cognition reached the same place earlier with SWE-grep (Oct 2025).
- [P] **Both vendors train models for their own harness.** Cursor: Tab (online RL), Composer 1/2/2.5 (RL inside the Cursor agent harness, Composer 2/2.5 built on Kimi K2.5), plus Grok models with SpaceXAI. Cognition: SWE-1.x, SWE-2 (post-trained from Kimi K3), SWE-2 Flash (from Thinking Machines' Inkling-Small, released today), SWE-grep for retrieval.
- [P] **Both moved to coordinator/worker multi-agent designs in 2026**, and both keep the "one writer" rule in some form. Cursor Projects (Sep 10, 2026): a coordinator "doesn't write code itself." Cognition's Walden Yan (Apr 22, 2026): multi-agent works "when writes stay single-threaded."
- [P] **Cognition's harness bet is model mixing.** Devin Fusion pairs a frontier "lead" with a cheap "sidekick" in one task; Cognition reports about 31-39% lower cost per task than Claude Code or Codex on the same lead model (vendor-run, Artificial Analysis figures). Their line: "models ... should be evaluated on price per task rather than price per token."
- [P] **Windsurf is gone as a brand.** It became Devin Desktop on Jun 2, 2026. Cascade is now the "legacy" agent; the default local agent is "Devin Local," the same harness as Devin CLI.
- [P] **Cloud execution with VM isolation is the default story for both.** Devin: each session in its own VM, hypervisor-level snapshots, "Containerized agents can't complete real engineering work." Cursor: cloud agents in isolated VMs, plus Self-Hosted Machines (Sep 2, 2026) where tools run inside your network but inference stays in Cursor's cloud.
- [P] **Local sandboxing:** Cursor uses Seatbelt (macOS) and Landlock + seccomp (Linux), network blocked by default; Devin CLI uses bubblewrap on Linux and has no Windows sandbox.
- [P] **Cursor is building the whole SDLC stack:** Origin code hosting (GitHub alternative, Aug 17 beta), Bugbot, Security Review, Rollouts, Agent SDK (GA Oct 20). Cognition is doing the same from the other end: Devin Review, Devin Security (Corridor acquired Oct 28), Auto-Triage.

---

## Part A: Cursor (Anysphere, a SpaceX subsidiary)

### A1. What it is, ownership, pricing, surfaces

| Item | Fact | Tag / source |
|---|---|---|
| Maker | Anysphere. SpaceX announced an all-stock purchase valued at $60B on Jun 16, 2026 (BNN: expected close Q3 2026; in April SpaceX had taken an option to buy for $60B or pay $10B for a partnership); Cursor's blog says the acquisition closed: "officially been acquired by SpaceX" (Aug 14, 2026), completing "the acquisition process that started in April" | [S] deal terms (BNN Bloomberg); [P] closing (https://cursor.com/blog/joining-spacex) |
| License | Closed source (VS Code fork plus proprietary agent, models and cloud) | [O] from product structure; no open-source license found |
| Plans (Nov 2026) | Free; Plus $8 (Grok models only); Premium $30 (4x Plus pool, third-party models at API list price); Super $100 (15x); Ultra $200 (50x); Teams $30+/user; Enterprise custom. One weekly pool shared across Cursor and Grok (Chat, Imagine, Voice, Bot) | [P] https://cursor.com/pricing |
| Regional plan | "Cursor Start", ₹649/month in India, Jul 28, 2026 | [P] changelog page 3 |
| Surfaces | Desktop IDE (VS Code fork), Agents Window (Cursor 3, Apr 2, 2026), CLI (`agent`), web (cursor.com/agents), iOS (beta Jun 29, 2026), iPad (Jul 29, 2026), Android via PWA, Slack, GitHub/GitLab/Bitbucket comments, Linear, API, Agent SDK, ACP server for JetBrains/Zed/Neovim | [P] docs/cloud-agent, changelog, docs/cli/acp |
| Revenue | "Cursor Recurring Revenue Doubles in Three Months to $2 Billion" (Bloomberg headline, Mar 2, 2026, linked from Cursor's press section) | [S] |
| Internal agent share | "Thirty-five percent of the PRs we merge internally at Cursor are now created by agents operating autonomously in cloud VMs." Agent users outnumber Tab users about 2:1 ("we now have 2x as many agent users as Tab users," flipped from about 2.5x Tab users in Mar 2025) (Michael Truell, Feb 26, 2026) | [P] https://cursor.com/blog/third-era |

[R] One FAQ page found in search says SpaceX does not own Cursor. Cursor's own Aug 14 post says otherwise.

### A2. Agent loop architecture

- [P] Single agent loop with "no limit on the number of tool calls Agent can make during a task" (https://cursor.com/docs/agent/overview). Checkpoints snapshot files before significant changes; they are local and separate from git.
- [P] **Steering**: a follow-up "is delivered at the agent's next tool call instead of cutting off work mid-action." **Side chats** (`/side`, `/btw`, v3.11, Jul 10, 2026). **`/goal`** sets a long-lived objective; `/loop` reruns a prompt or skill on an interval (Aug 19, 2026 changelog).
- [P] **Modes**: Agent, Ask (read-only), Plan, plus Debug Mode and Design Mode (browser element selection with voice, Jun 5, 2026) and custom modes (any skill pinned as "always on", Aug 19, 2026).
- [P] **Plan Mode** (Shift+Tab): asks clarifying questions, researches the codebase, writes a markdown plan saved in the home directory by default ("Save to workspace" to keep it), then "Click to build." Docs advise reverting and refining the plan rather than patching with follow-ups (https://cursor.com/docs/agent/plan-mode). Slack also now "responds with a plan before it begins" (Jul 17, 2026).
- [P] **Subagents**: built-in Explore (faster model, parallel searches) and Browser. Custom subagents are markdown + YAML (`name`, `description`, `model`, `readonly`, `is_background`) in `.cursor/agents/`, and Cursor also reads `.claude/agents/` and `.codex/agents/`. "Subagents start with a clean context"; parent gets only the final summary; background subagents return immediately. Subagents share the checkout unless run in a worktree or cloud environment (https://cursor.com/docs/subagents). Since Aug 19, 2026 each cloud subagent can get its own machine; SDK subagents can nest to any depth (Jun 4, 2026).
- [P] **Projects** (beta, Sep 10, 2026): "The coordinator doesn't write code itself but directs other agents that do." It "delegates tasks to thousands of subagents," runs in the cloud, starts a local agent when something must run on your machine, keeps shared context files synced across machines, and can "watch a Slack channel, run on a schedule, or follow all your PRs, fixing CI" (Alexi Robbins and Fredrika Lindh, https://cursor.com/blog/projects). The post does not say how a Project decides it is done. [Verified 2026-11-04: coordinator and "thousands of subagents" quotes matched raw page.]
- [P] **Research lineage** (Wilson Lin, "Towards self-driving codebases", Feb 5, 2026, older than 6 months): shared-file locking failed ("Locking is easy to get wrong and narrowly correct, and more prompting didn't help"); a central integrator became a bottleneck and was removed; final design is recursive planners that do no coding plus workers that own a slice and hand results up. Lessons: "Constraints are more effective than instructions"; concrete ranges like "Generate 20-100 tasks" beat vague scope (https://cursor.com/blog/self-driving-codebases).
- [P] **Verification**: cloud agents "produce merge-ready PRs with artifacts to demo their changes" (screenshots, video, logs) and can use a remote desktop and browser (https://cursor.com/docs/cloud-agent). Rollouts (Sep 23, 2026) write a monitoring plan per PR and report healthy / regression / inconclusive after deploy; they can open revert PRs but do not roll back on their own.
- [P] **Background / async**: cloud agents (handoff with `&` prefix in the CLI, `/in-cloud`, `/babysit` for PR prep, Jun 17, 2026), Automations triggered by Slack emoji, GitHub events, cron (v3.8, Jun 18, 2026), remote control of local agents from iOS (Oct 6, 2026).

### A3. Tools, edit format, search

- [P] Documented built-in tools: search files and folders, web search, fetch rules, read files (images too), edit files ("Suggest edits to files and apply them automatically"), run shell commands, browser ("take screenshots, test applications, and verify visual changes"), image generation, ask questions (https://cursor.com/docs/agent/tools). Also canvases (interactive shareable outputs from cloud agents, Oct 16, 2026) and computer use on self-hosted Linux and Mac (Sep 2, 2026).
- [P] Tools held in static context after the Sep 2026 trim: read, search, edit, shell, plus `ask_question` and `create_plan`. Everything else (background shell monitoring, cloud subagents, web, all MCP tools) is loaded dynamically (https://cursor.com/blog/improved-token-efficiency).
- **Edit format.** Current docs do not describe it. [P] History: Cursor's "fast apply" model (Aman Sanger, May 14, 2024, older than 6 months) rewrote the whole file with a fine-tuned Llama-3-70B and "speculative edits," about 1,000 tokens/s, "up to 9x faster" than their earlier GPT-4 deployment. Reasons given against diffs: "Diffs force the model to think in fewer tokens" and "models have likely seen more full-files of code than diffs of code" (https://cursor.com/blog/instant-apply). [S] 2025 community-extracted prompts show an `edit_file` tool whose `code_edit` was passed to a separate apply model. [O] Do not claim on a slide what Cursor's 2026 edit tool looks like; no primary source says.
- [P] **Read tool change** (Sep 23, 2026): line numbers now on every tenth line instead of every line; cut cache-read tokens 1.6% "with no reduction in quality" ([R] earlier draft quoted "with no quality loss"; not the page's wording).
- **Code search: big change.**
  - [P] Nov 6, 2025 (older than 6 months): Cursor trained its own embedding model on agent traces and reported "on average 12.5% higher accuracy in answering questions (6.5%–23.5% depending on the model)"; "Semantic search is currently necessary to achieve the best results, especially in large codebases" (https://cursor.com/en-US/blog/semsearch).
  - [P] Mar 23, 2026: "Instant Grep," a local n-gram index for regex ([R] "trigram" -> the post walks through classic trigram indexes, then says its approach is "called Sparse N-grams"), because "the agents just love to use grep" and "We routinely see rg invocations that take more than 15 seconds" (Vicent Martí, https://cursor.com/blog/fast-regex-search).
  - [P] July 2026, Cursor staff on the forum (all posters below carry the staff flag in the thread's JSON): the older semantic path "was rapidly no longer helping in a meaningful way" (maximep, Jul 21); "Semantic/embeddings indexing is being turned down in favor of grep-based retrieval" (Colin, Community Support Engineer, Jul 22); the index lives in `.git/cursor/`, is anchored to a git commit, "about half the size of the source it indexes," and non-git projects fall back to "plain ripgrep" (Colin, Jul 28); search path has "no embeddings involved anywhere in it" (mohitjain, Jul 31). Current docs: Cursor "does not store embeddings of your codebase for search" (https://cursor.com/docs/context/semantic-search; forum thread URL in frontmatter).
  - [R] Any slide saying "Cursor uses an embeddings index / vector RAG over your repo" is stale as of July 2026.
  - [P] LSP: Cursor 3 code navigation has "go to definition in the editor with full LSPs" (https://cursor.com/blog/cursor-3; [R] earlier draft quoted "supported by full LSPs," not on the page).

### A4. Context, instructions, memory, compaction

- [P] **Rules** (https://cursor.com/docs/context/rules): `.cursor/rules/*.mdc` with frontmatter `description`, `globs`, `alwaysApply`. Four types: Always Apply, auto-attached by glob, agent-requested (description only), manual (`@`-mention). `AGENTS.md` at root and nested in subdirectories ("more specific instructions taking precedence"). User Rules in settings. Team Rules from the dashboard; admins can enforce them. Order: Team, then Project, then User; "earlier sources take precedence when guidance conflicts." The rules page does not mention `CLAUDE.md`.
- [P] Skills (`SKILL.md`), commands (markdown), plugins bundling all of these, Customize page at user/team/workspace level (v3.9, Jun 22, 2026).
- [P] **System prompt trimmed by about 66%** (Sep 23, 2026; Jediah Katz, Connor O'Keefe and Calvin Yee): "roughly 66% of our system prompt." Removed what the post calls "long lists of 'DO NOT do this,' 'You must,' or 'Important' instructions" written for weaker models; now defines how each tool behaves and relies on the model. Overall: "reduced token costs for users by 7% without reducing agent quality" (https://cursor.com/blog/improved-token-efficiency).
  - [R] Earlier draft said the prompt trim was "validated by A/B tests on live traffic" and quoted "long lists of prohibitions and emphasis markers" and "evals often focus on hard problems that don't match real traffic." Correction: neither quote is on the page. The post describes A/B tests for the tool-loading configurations ("we A/B tested several configurations based on how often each tool was used") and says in general that A/B tests on a large user base are "crucial" because evals "often represent 'hard' problems and don't properly reflect the true distribution of user requests." It does not say how the 66% trim itself was validated. [O] This is a vendor data point for the deck's thin-harness thesis; compare `track2-thin-harness-evidence.md`.
- [P] **Prompt caching**: since GPT-5.6, Cursor sets explicit cache breakpoints after stable layers; request-specific context (skills, subagents, environment) moved into a "phantom user message" past the cache boundary; cold cache misses down 20%. "Breakpoints only help if the prefix itself stays stable."
- [P] Cursor removed prompt instructions that pushed the agent toward subagents for exploration, citing a "coordination tax" of duplicated work; "agents choose a different model only when directed by the user or the harness."
- [P] **Compaction trained into the model**: "self-summarization" (Federico Cassano and Sasha Rush, Mar 17, 2026). The model writes its own summary near the context limit during RL and the summary is rewarded with the outcome. "Self-summary consistently reduces the error from compaction by 50%"; summaries average about 1,000 tokens versus "more than 5,000 tokens" for "a highly tuned prompt-based compaction baseline." Rationale: harness compaction "can cause the model to forget critical information" (https://cursor.com/blog/self-summarization). A `preCompact` hook exists.
- [P] Memory: Projects keep shared context files ("Each Project maintains a set of files that sync across every cloud and local machine its agents use"; [R] the earlier quote "grow with the Project" did not match the raw page); changelog mentions deletable "memory files" in Automations (Jun 18, 2026). [E] No standalone memory doc was fetched.
- [P] Context window: depends on model; Grok 4.7 is 256k with a 500k option (https://cursor.com/docs/models).

### A5. Safety: approvals, sandbox, network

- [P] **Run modes** (https://cursor.com/docs/agent/security/run-modes):
  - Auto-review (recommended): allowlisted calls run; other shell commands run in the sandbox; calls that cannot be sandboxed go to a classifier (Gemini 3.5 Flash Lite, fallback Claude 4.5 Haiku) that covers shell, MCP and Fetch. "The classifier can make mistakes"; it is not a security boundary. Plain-English `allow_instructions` / `block_instructions` in `permissions.json`.
  - Allowlist: only allowlisted actions skip approval; sandbox optional.
  - Run Everything: no sandbox, no classifier.
- [P] **Sandbox tech**: macOS Seatbelt via `sandbox-exec` (Cursor 2.0+); Linux Landlock + seccomp, kernel 6.2+ with Landlock v3, else falls back to asking approval. Windows sandboxing is not described on the page.
- [P] **Network**: "Blocked by default, then opened by your network mode and `sandbox.json`." Default mode is your allowlist plus Cursor's defaults (GitHub, npm, PyPI, crates.io). Protected paths like `.git/hooks` and `.vscode`. "Team-admin policies and Cursor's hardcoded security rules layer on top, so local files cannot weaken those protections." Run modes do not apply to cloud agents.
- [P] CLI permissions use tokens `Shell(git)`, `Read(glob)`, `Write(glob)`, `WebFetch(domain)`, `Mcp(server:tool)`; deny beats allow (https://cursor.com/docs/cli/reference/permissions).
- [P] Hooks can block: exit code 2 denies (matches Claude Code), other failures are "fail-open by default" unless `failClosed: true`; "any `deny` wins over `ask`, and `ask` wins over `allow`" (https://cursor.com/docs/hooks).
- [P] Self-Hosted Machines (Sep 2, 2026): worker "opens a long-lived outbound HTTPS connection to the Cursor cloud"; "Cursor never initiates a connection into your network." But "Tool outputs flow back to Cursor for inference and may contain code" (https://cursor.com/blog/self-hosted-machines).
- [P] Incident, Oct 29, 2026: malicious versions 2.1.312 and 2.1.313 of the `Anthropic.claude-code` extension were served from Cursor's VS Code extension marketplace for about 11 hours, attempting an SSH backdoor; Cursor shut the marketplace down, rotated keys and rebuilt it (https://cursor.com/blog/claude-code-extension-security-notice).
- Earlier sandbox escapes in Cursor are recorded in `round2-agent-security-governance.md`.

### A6. Extensibility

- [P] MCP (dynamic loading; team MCPs in marketplaces, v3.10 Jun 30, 2026), skills, subagents, commands, hooks (18 agent events plus Tab hooks; loads Claude Code hooks), plugins and team marketplaces, MCP Apps.
- [P] CLI: `agent`, headless `agent -p ... --output-format`, plan and ask modes, `&` to send to cloud, GitHub Actions doc, ACP server (`agent acp`) with Cursor extension methods `cursor/ask_question`, `cursor/create_plan` (https://cursor.com/docs/cli/overview, /cli/acp).
- [P] **Agent SDK** (GA Oct 20, 2026, Rustam Lalkaka): "The Agent SDK is generally available today." An agent is defined in code like a small project (Markdown prompts, TypeScript tools, service connections, evals); "supports evals and event replay out of the box"; `agent-sdk deploy` to Cursor's infrastructure, or run on your own as "a single Node process that can be packaged in a container." [E] The folder names `instructions.md`, `tools/`, `skills/`, `mcp-connections/`, `channels/` and the commands `agent-sdk eval` and `agent-sdk github replay <pr-url>` are NOT in the blog post (raw-HTML search, 2026-11-04); they may come from SDK docs not cited here. Verify before using. It is the framework Cursor uses for Bugbot, Security Review and Rollouts. "The most useful agents are tailored to how a particular team operates" (https://cursor.com/blog/agent-sdk). There is also a separate TypeScript/Python SDK for driving the Cursor agent.
- [P] Cloud environments: snapshot, agent-led setup, or Dockerfile via `.cursor/environment.json`; "Builds" (Aug 13, 2026) pre-warm environments; Environments API beta and up to 300 repos per environment (Oct 16, 2026).
- [P] **Bugbot**: reviews PR diffs on each push; effort levels; rules in `.cursor/BUGBOT.md` (Cursor's `.mdc` rules do not apply); learned rules from merged/closed PRs and `@cursor remember`; Autofix spawns a cloud agent (https://cursor.com/docs/bugbot). Jun 10, 2026: now on Composer 2.5, review time about 90 s (from about 5 min), 0.62 bugs per review (from 0.56), about 22% cheaper per run.

### A7. Model coupling and in-house models

| Model | Date | What Cursor says | Tag |
|---|---|---|---|
| Fast apply (Llama-3-70B fine-tune) | May 2024 | whole-file rewrite with speculative edits | [P] older than 6 months |
| Tab | Sep 12, 2025 | online RL; "over 400 million requests per day"; 21% fewer suggestions, 28% higher accept rate; new checkpoints every 1.5-2 hours | [P] older than 6 months |
| Composer (1) | Oct 29, 2025 | "During RL, we want our model to be able to call any tool in the Cursor Agent harness"; "hundreds of thousands of concurrent sandboxed coding environments"; "generation speed four times faster than similar models" | [P] older than 6 months |
| Composer 2 | Mar 19, 2026 | "our first continued pretraining run"; CursorBench 61.3; $0.50/$2.50 per M tokens | [P] |
| Composer 2 base | Mar 20-23, 2026 | Built on Moonshot's Kimi K2.5, not disclosed at launch. Aman Sanger: "It was a miss to not mention the Kimi base in our blog from the start." | [S] VentureBeat and others |
| Composer 2.5 | May 18, 2026 | same Kimi K2.5 checkpoint, disclosed; 25x more synthetic tasks; RL with "targeted textual feedback"; fast variant is the default ($3/$15) | [P] |
| From-scratch model | stated May 18, 2026; Compile, Jun 2026 | Composer 2.5 post: "Together with SpaceXAI, we're training a significantly larger model from scratch, using 10x more total compute." ([R] earlier draft quoted "a much larger model"; page says "significantly larger.") Press: about 1.5T params on 100k+ GPUs | [P] intent; [S] size |
| Grok 4.6 / 4.7 | Aug / Sep 21, 2026 | Cursor's models page calls Grok 4.7, 4.6, 4.5 and Composer 2.5 "Cursor's own models" ([R] the label "with SpaceXAI" is not on the models page). The x.ai post says Grok 4.7 was trained "to natively understand the Grok Bot harness" [P*] and "uses a new, larger base model compared to Grok 4.6" [P]; it does not say "from scratch." [R] "x.ai credits SpaceXAI" -> the x.ai page is branded "SpaceXSI" and its footer credits "SpaceX Super Intelligence LLC"; it never says SpaceXAI. Cursor's own posts use "SpaceXAI" | [P] |
| Cursor Router (Auto) | Jul 22, 2026 | routes each request; modes Intelligence / Balance / Cost; admin allow/block lists | [P] |

- [R] "Composer 3 launched Jun 16, 2026 as a 1.5T from-scratch model": only aggregator sites say so and they contradict each other (one says "rumored," Aug 8). Cursor's own models page on 2026-11-04 lists no Composer 3. Whether the from-scratch model shipped under another name (for example as a Grok version) is not stated by Cursor or x.ai. Open question.
- [P] Third-party models remain: Anthropic (incl. Opus 5.5, Fable 5.1, Sonnet 5.5), OpenAI (GPT-5.x through 5.6 Sol/Terra/Luna), Google (Gemini 3.x, Gemini 4 Argon), Moonshot, DeepSeek, Meta Muse, Z.ai (https://cursor.com/docs/models). [O] Since the SpaceX deal the cheap tiers are Grok-only, so model-agnostic now has a price attached.

### A8. Philosophy (Cursor, from their own writing)

- [P] Michael Truell, Feb 26, 2026: "Cursor is no longer primarily about writing code. It is about helping developers build the factory that creates their software." And: "The human role shifts from guiding each line of code to defining the problem and setting review criteria." (https://cursor.com/blog/third-era)
- [P] Truell and Sualeh Asif, Apr 2, 2026: "We will also continue to invest in the IDE until codebases are self-driving." (https://cursor.com/blog/cursor-3)
- [P] Speed as a design goal (Oct 29, 2025, older than 6 months): "response speed is a critical component for interactive development," so Composer was rewarded for efficient tool use and parallel calls (https://cursor.com/blog/composer). Composer 2.5: "fast is the default option."
- [P] Train the model inside the product harness: "During RL, we want our model to be able to call any tool in the Cursor Agent harness" and RL infrastructure "enabled seamless unification of RL environments with production environments" (https://cursor.com/blog/composer).
- [P] Measure on real traffic, not hard evals: evals "often represent 'hard' problems and don't properly reflect the true distribution of user requests," so "Leveraging A/B tests on a large user base is crucial" (Sep 23, 2026, token-efficiency post). ~~evals "often focus on hard problems that don't match real traffic"~~ [R] paraphrase that was presented as a quote.
- [P] Change the infrastructure, not the agent: "the agents just love to use grep," so Cursor indexed grep rather than steering agents away from it (Mar 23, 2026).
- [P] Multi-agent research principles (Wilson Lin, Feb 5, 2026): "The system should be anti-fragile"; "Empirical over assumption-driven"; "Design for throughput explicitly"; "Constraints are more effective than instructions."
- [P] Agent SDK (Rustam Lalkaka), Oct 20, 2026: "The most useful agents are tailored to how a particular team operates."
- **What they reject, stated:** heavy prohibition-style prompts for modern models (token post); shared-file locking and a central integrator for agent swarms (self-driving codebases); semantic embeddings for search (forum, Jul 2026); prompt-based compaction (self-summarization post).

### A9. Direction (last 6 months, shipped or stated)

| Date (2026) | Shipped |
|---|---|
| May 18 | Composer 2.5 |
| Jun 4 | SDK custom tools, auto-review, nested subagents |
| Jun 10 | Bugbot on Composer 2.5, `/review` |
| Jun 16-17 | SpaceX deal announced; Compile conference: from-scratch model, Origin, mobile [S] |
| Jun 17-18 | Cloud env setup by agent, `/in-cloud`, `/babysit`; Automations triggers |
| Jun 22-30 | Customize page, iOS app beta, team MCP marketplaces |
| Jul 10 | Side chats, conversation search, cloud agent hooks |
| Jul 22 | Cursor Router powers Auto |
| ~Jul 21 | Embeddings index turned down; Instant Grep only [P forum] |
| Aug 13 | Builds (3x faster cloud starts), AIUC-1 cert, Firetiger acquired |
| Aug 14 | Acquisition by SpaceX closes |
| Aug 17 | Origin code hosting, early beta, all paid plans |
| Aug 19 | Subscriptions, custom modes, subagents on own machines, `/goal`, steering |
| Aug 27 | Cloud agents without a repo (creates an Origin repo) |
| Sep 2 | Self-Hosted Machines (My Machines, team pools; runtimes incl. AWS Lambda, Coder, Daytona, Modal, E2B) |
| Sep 10 | Projects (coordinator + thousands of subagents) |
| Sep 21 | Grok 4.7 in Cursor |
| Sep 23 | Rollouts, Security Review; token-efficiency harness changes |
| Oct 6 | Remote control of local agents from iOS |
| Oct 13 | Origin App Marketplace |
| Oct 16 | Canvases, Environments API beta |
| Oct 20 | Agent SDK GA |

Stated next: [P] apply token learnings "to Grok Bot's harness" (Sep 23 post); [P] the from-scratch SpaceXAI model, expected to be "a major leap" (May 18 post); [P] Compile on the Road in New York Nov 5, Amsterdam Jan 27 (https://cursor.com/compile); [S] Origin public launch planned for fall 2026.

---

## Part B: Cognition (Devin, Devin Desktop, ex-Windsurf)

### B1. What it is, pricing, surfaces

| Item | Fact | Tag / source |
|---|---|---|
| Company | Cognition, founded Jan 2024. Acquired Windsurf product, IP and brand Jul 14, 2025 (older than 6 months) | [P] founding: https://cognition.com/blog/1b-run-rate; Windsurf date: inferred from "One year ago today" in the Jul 14, 2026 post https://cognition.com/blog/one-year-of-building-together (the 1b-run-rate post does not give it) |
| Brand change | Windsurf became **Devin Desktop**, Jun 2, 2026 (Scott Wu and Jeff Wang): "the next generation of Windsurf," "fully backwards-compatible with Windsurf." The launch post does not mention Devin Local or Cascade; those come from the Devin Local docs (B2) | [P] https://cognition.com/blog/introducing-devin-desktop |
| Products | Devin (cloud agent in its own VM), Devin Desktop (IDE with Agent Command Center), Devin CLI (Apr 27, 2026), Devin Review (Jan 21, 2026), Devin Security, Auto-Triage, DeepWiki / Ask Devin, Devin API, scheduled sessions and Automations | [P] blog index, docs |
| License | Closed source. SWE-2 Flash weights withheld over cyber risk ("so we are not sharing the weights publicly yet"), with a planned program "to securely share the weights with industry partners and researchers" ([R] "because of cyber misuse risk" was a paraphrase in quote marks) | [P] https://cognition.com/blog/swe-2-flash |
| Pricing | Free; Pro $20/mo (frontier models from OpenAI, Claude, Gemini, SpaceXAI, open models; SWE-2 free; Devin Cloud); Max $200/mo; Teams $80/mo + $40 per dev seat (up to 200 users); Enterprise custom (VPC and dedicated deployment) | [P] https://devin.ai/pricing |
| Revenue | $1B annualized run rate (Sep 25, 2026); Series E over $2B at $48B (Sep 8, 2026); team "grew from 44 to 350 people" in the year after the merger | [P] run rate: 1b-run-rate; raise: series-e; headcount: one-year-of-building-together (not the 1b-run-rate post) |
| Named customers | NVIDIA, GE Aerospace, Citi, Mercedes-Benz, Modal; partnership with LTM on "cyber risk in financial services" (Jul 28, 2026) | [P] series-e, blog index |
| Government | FedRAMP High "in-process" (Jul 13, 2026) | [P] blog index |

### B2. Agent loop architecture

- [P] **Devin (cloud)**: runs in "a Linux-based virtual machine with your repositories cloned, tools installed, dependencies resolved." Environments are YAML "blueprints" built into a "frozen, bootable image"; "Session changes don't persist back to the snapshot." Windows and macOS snapshots can be added (https://docs.devin.ai/onboard-devin/environment.md). Windows PC (May 21, 2026) and Android emulators (May 13, 2026).
- [P] **Devin 2.2** (Feb 24, 2026): "It plans, codes, reviews its own output, catches issues, and fixes them - all before you ever open the PR"; full Linux desktop for computer use; 3x faster startup.
- [P] **Managed Devins** (Mar 19, 2026): "Each managed Devin is a full Devin, running in its own isolated virtual machine"; "The main Devin session acts as a coordinator"; ~~children coordinated "through an internal MCP"~~ [R] not on the page (raw-HTML search 2026-11-04); the page says the coordinator can "send instructions, context, or corrections to any managed Devin mid-task"; "Devin can also read the full trajectories of its managed Devins" and track ACU consumption per child.
- [P] **Devin Local** (in Devin Desktop and Devin CLI): "our next-generation agent harness shared with Devin CLI." Modes Code, Smart, Ask, Plan, Bypass Permissions. Foreground and background subagents that "share tools and codebase context with the parent agent"; custom subagents at `agents/<name>.md`; a Quick Review subagent; worktrees; "built around prompt caching" (https://docs.devin.ai/desktop/devin-local/overview.md). Cascade is "the legacy Cascade agent" and admins can disable it.
- [P] **Fusion** (Jun 29, 2026; local Sep 11, 2026): two parallel agents, a frontier lead and a cheaper sidekick, each with its own tools and cached context. The lead plans, interprets ambiguity and reviews; "The lead always reviews the work, identifies problems, and can take control back when the sidekick is out of its depth." (that sentence is on the local-fusion post). Model switches happen "during context compaction, which would trigger a cache miss anyway" (devin-fusion post; [R] earlier draft quoted "which already causes a cache miss," not the page's wording). "Instead of passing entire conversations between models, the lead and sidekick only exchange briefs, results, and feedback" (local-fusion) (https://cognition.com/blog/devin-fusion, https://cognition.com/blog/local-fusion).
- [P] **Adaptive**: a separate per-request router at a flat $0.50 / $2.00 per M tokens; docs recommend Fusion for most users (https://docs.devin.ai/cli/adaptive.md).
- [P] **Verification** (Ido Pesok, May 29, 2026): "Devin will spin up the app, click through it, and confirm its changes actually work"; test plan "must be grounded in source, not assumptions"; login steps moved into deterministic scripts in the repo ("helped decrease flakiness dramatically"); returns a report with screenshots and a chaptered video. Known gaps: missed toasts, using browser JavaScript instead of real clicks (https://cognition.com/blog/testing-development).

### B3. Tools and search

- [P] Devin Local tool categories in analytics: Code Edit, Run Command, Search Web, MCP Tool. Edit format is not documented ("an edit only runs after you approve it"). [O] No primary source for Cognition's edit format; do not put one on a slide.
- [P] **SWE-grep** (Oct 16, 2025, older than 6 months): RL-trained retrieval models behind the "Fast Context" subagent; restricted tools (grep, read, glob); "up to 8 parallel tool calls per turn," "in a maximum of 4 turns" (3 exploration, 1 answer); served on Cerebras at 2,800+ tok/s (mini) and 650+ tok/s; reward is weighted F1 favouring precision. On embeddings: "The embeddings can even be counterproductive, as the agent can give too much weight to irrelevant information" (https://cognition.com/blog/swe-grep).
- [P] Devin Desktop still lists "Context Awareness," a RAG-based codebase index with remote indexing for Teams/Enterprise, alongside Fast Context and Codemaps ("shareable hierarchical maps of your codebase", Nov 4, 2025) (https://docs.devin.ai/_llms/en/desktop.txt).
- [P] **DeepWiki** inside Devin: "automatically indexes your repos and produces wikis with architecture diagrams"; steerable with `.devin/wiki.json`; Ask Devin "will use information in the Wiki to better understand and find the relevant context in your codebase" (https://docs.devin.ai/work-with-devin/deepwiki.md). The public deepwiki.com and its MCP serve public GitHub repos.

### B4. Context, instructions, memory

- [P] **Devin CLI / Devin Local rule files** (https://docs.devin.ai/cli/extensibility/rules.md): `AGENTS.md` (recommended), `AGENTS.local.md`, `AGENT.md`, `.windsurfrules`, `CLAUDE.md`, `.devin/rules/*.md`, `.windsurf/rules/*.md`, `.cursor/rules/*.md|*.mdc`, `.claude/`, plus global `~/.config/devin/AGENTS.md` and `~/.claude/CLAUDE.md`. "Files at the workspace root are loaded at session start"; subdirectory files load lazily "when the agent accesses files in that directory." `.devin/` beats `.windsurf/`. Per-source toggles in `read_config_from`.
- [P] **Knowledge** (cloud Devin's trigger-retrieved notes) "is deprecated and will be removed in a future update"; it migrates to Skills in Plugins. It auto-imports `.rules`, `.mdc`, `.cursorrules`, `.windsurf`, `CLAUDE.md`, `AGENTS.md` (https://docs.devin.ai/onboard-devin/knowledge-onboarding.md). Devin CLI "does not yet support Knowledge, Playbooks, or Secrets from your Devin account."
- [P] Memories and rules with global, workspace and enterprise scopes remain in the Cascade/JetBrains plugin docs.
- [P] Compaction: SWE-1.7 (Jul 8, 2026) is trained for self-compaction (condense working state, resume from the summary), and "We use an alternating length penalty to incentivize concise output without sacrificing correctness" [P*] ([R] the earlier quote "self-compaction with an alternating length penalty" is a merge of a section title and a sentence, not page text). In Sep 2025 (older than 6 months) Cognition kept its own memory and compaction after finding Sonnet 4.5's self-written notes incomplete, and named "context anxiety": "we found the model taking shortcuts or leaving tasks incomplete when it believed it was near the end of its window" ([R] earlier quote "takes shortcuts or stops early" is not on the page) (https://cognition.com/blog/devin-sonnet-4-5-lessons-and-challenges).

### B5. Safety

- [P] Cloud: VM per session. "The industry consensus for running untrusted code is VM-level isolation." "Containerized agents share a kernel." Snapshotting "full machine state at the hypervisor level — memory, process trees, and filesystem" (https://cognition.com/blog/what-we-learned-building-cloud-agents).
- [P] **Devin CLI sandbox** (https://docs.devin.ai/cli/sandbox.md; all quotes in this bullet matched the raw doc 2026-11-04): Linux uses bubblewrap (`bwrap`) and `socat` ("Sandboxing requires `bubblewrap` (`bwrap`) and `socat` to be installed"); "OS-level sandboxing is not currently supported on Windows"; macOS mechanism not named. Off unless `--sandbox` or admin enforcement "Required." Writable: workspace plus `Write(...)` scopes, "everything else is read-only"; `Read(...)` deny rules hide paths. Network default is `"full"`; domain filtering through a loopback proxy and "Sandbox network filtering is currently unstable." Fails closed: "the CLI will refuse to start rather than running unsandboxed."
- [P] Permissions: allow / ask / deny rules, MCP tool permissions, enterprise network enforcement (Devin Local docs).
- [P] Jack Cable (Cognition), Nov 3, 2026: move agents off laptops; "Remote dev boxes and cloud agents run in an environment you control, can be given only the access a specific task needs"; "Wherever possible, remove production secrets from developer machines" (https://cognition.com/blog/practical-guide-to-security-november-2026).

### B6. Extensibility

- [P] MCP (stdio, HTTP, SSE; Devin MCP Marketplace since Jul 2025), skills, plugins, hooks (lifecycle hooks in CLI), custom subagents, workflows (markdown slash commands), Devin API, scheduled sessions, Automations.
- [P] **ACP**: Devin Desktop runs "Any ACP-compatible agent ... inside Devin Desktop alongside Devin" in the Agent Command Center; Devin CLI has ACP integrations for JetBrains, Zed and Xcode (docs index).
- [P] Devin Review, Devin Security (Oct 26, 2026: deep scans powered by "Claude Mythos and other frontier cyber models"; "Devin can run thousands of parallel sessions in independent virtual machines"; "Each proposal requires human approval"; "Devin Security is model-neutral").

### B7. Model coupling and in-house models

| Model | Date | Base | Claim | Tag |
|---|---|---|---|---|
| SWE-grep / mini | Oct 16, 2025 | not stated | retrieval subagent, Cerebras | [P] older than 6 months |
| SWE-1.6 | Apr 7, 2026 | not fetched | "Improving Model UX" | [E] title only |
| SWE-1.7 | Jul 8, 2026 | Kimi K2.7 | Cerebras at 1000 TPS; FrontierCode 1.1 42.3% vs Opus 4.8 46.5% | [P] |
| SWE-2 | Sep 10, 2026 | Kimi K3 (2.8T) | one RL run across effort levels with cost-penalised reward; Terminal-Bench 2.1 92.8%, Terminal-Bench 4.0 27.3% (vs GPT-6 Astra 57.9%) | [P] |
| SWE-2 Flash | Nov 4, 2026 | Thinking Machines Inkling-Small (276B / 12B active) | about 200 tok/s vs 60 for SWE-2, one-fifth the cost; "a fully American coding model" ([R] earlier "fully American-developed" is not the page's wording); weights withheld; free through Nov 30 | [P] |

- [P] Model-agnostic by stated policy: "We can choose and combine the models best suited to the work, including our own, rather than tie customers to one provider" (https://cognition.com/blog/series-e). The Fusion post notes Fable 5 access was suspended on Jun 12, 2026 [E]; Sep posts use Fable 5.1 again.
- [O] All Cognition benchmark numbers above are vendor-run, often on Cognition's own FrontierCode suite. See `round2-evals-and-benchmarks.md` §6.

### B8. Philosophy (Cognition, from their own writing)

- [P] Walden Yan, "Don't Build Multi-Agents" (Jun 12, 2025, older than 6 months; the libraries named are OpenAI's Swarm and Microsoft's AutoGen): principles "Share context, and share full agent traces, not just individual messages" and "Actions carry implicit decisions, and conflicting decisions carry bad results." Context engineering "is effectively the #1 job of engineers building AI agents." "The simplest way to follow the principles is to just use a single-threaded linear agent." Swarm/AutoGen-style libraries "actively push concepts which I believe to be the wrong way of building agents." (https://cognition.com/blog/dont-build-multi-agents)
- [P] Walden Yan, "Multi-Agents: What's Actually Working" (Apr 22, 2026), the follow-up (the swarm sentence on the page opens "We think the unstructured-swarm approach..."): "A lot has changed since then." "To start, models have become way more naturally “agentic.”" What works: clean-context reviewers ("we found this technique to work best when the coding and review agents do not share any context beforehand"), "smart friend" escalation, managers, read-only subagents. Rule kept: "multi-agent systems work best today when writes stay single-threaded" and extra agents "contribute intelligence rather than actions." Rejected: "the unstructured-swarm approach, arbitrary networks of agents negotiating with each other, is mostly a distraction." Open problem: "The open problems are all communication problems." (https://cognition.com/blog/multi-agents-working)
- [P] Cost per task: "models (and model-harness combos) should be evaluated on price per task rather than price per token"; "using more expensive models can make the entire system cheaper" (Sep 11, 2026, local-fusion post, no named author). "The age of using one model for all of your work is coming to an end" (Jun 29, 2026, The Cognition Team). "Opus behaves like a micromanager with an intern; Fable is a manager with a capable engineer" (Joon Hee Lee, Jul 13, 2026). ~~"When the judgment is the deliverable, delegating it backfires."~~ [R] not on the page; closest real line: "What will remain worth frontier prices is judgment: what to build, what to constrain, and who should write it," and "A model coerced into delegating doesn't gain that judgment."
- [P] Infrastructure: "Containerized agents can't complete real engineering work"; "Very few of these changes can be designed in advance" (Apr 23, 2026, The Cognition Team).
- [P] Outcomes: "The industry needs to move from maximizing usage metrics to maximizing outcomes" (Scott Wu, Jun 4, 2026). The AI Productivity Guarantee credits enterprise customers up to $10M if agent-estimated hours of merged work fall short of spend.
- [P] Role of engineers: "Human engineers will increasingly act as architects, setting goals and priorities"; "agents will become proactive by default, software will improve itself" (Sep 8, 2026).
- [P] Harness-model coupling: rebuilding for Sonnet 4.5 because it behaved differently "in ways that broke our assumptions about how agents should be architected" (Sep 29, 2025, older than 6 months).

### B9. Direction (last 6 months, shipped or stated)

| Date (2026) | Shipped |
|---|---|
| May 13 / 21 | Android emulators; Windows PC for Devin |
| May 18 | Auto-Triage |
| May 27 | Series D (blog title "More Devins in More Places") |
| Jun 2 | Devin Desktop replaces Windsurf brand |
| Jun 4 | AI Productivity Guarantee |
| Jun 8 | FrontierCode benchmark |
| Jun 29 | Devin Fusion |
| Jul 1-2 | Devin Security Swarm, remediation program |
| Jul 8 | SWE-1.7 |
| Jul 13 | FedRAMP High in-process |
| Jul 20-23 | TierZero and The Interaction Company acquired |
| Sep 8 | Series E, $48B |
| Sep 10 | SWE-2; Dioxus acquired |
| Sep 11 | Fusion in Devin Desktop and CLI |
| Sep 15 | AWS partnership |
| Sep 25 | $1B run rate |
| Oct 26-28 | Devin Security relaunch; Corridor acquired; FrontierCode 2.0 |
| Nov 4 | SWE-2 Flash (free through Nov 30) |

Stated next: [P*] SWE-2: "We're also rolling it out on Devin Web and Fusion" ([R] earlier quote "rolling out to Devin Web and Fusion" was not verbatim); [P] SWE-2 Flash weight-sharing program, "More on this in a few weeks"; [P] sandbox docs: "A future Strict mode may lock down sandbox configuration entirely" ([R] earlier quote "is not yet available" is not on the page); [P] "agents will become proactive by default" (Series E); [P] Corridor founders: "The next 6–12 months represent the most consequential period in the history of cybersecurity."

---

## Part C: Side by side

| Dimension | Cursor | Cognition |
|---|---|---|
| Primary surface | IDE + Agents Window, cloud agents, CLI, mobile | Cloud Devin in VMs; Devin Desktop and CLI for local |
| Loop | Single loop + subagents; Projects coordinator (no code) + workers | Single loop + subagents; manager Devin + child Devins in own VMs; Fusion lead + sidekick |
| Search | Instant Grep (local sparse n-gram index), Explore subagent; embeddings removed Jul 2026 | SWE-grep Fast Context subagent; DeepWiki; RAG Context Awareness still listed in Desktop |
| Compaction | Trained into Composer ("self-summarization") | Own compaction; SWE-1.7 trained with self-compaction |
| Instructions | `.cursor/rules/*.mdc`, AGENTS.md nested, team rules; reads `.claude/agents` | AGENTS.md first; reads `.cursor/rules`, `.windsurf`, `CLAUDE.md`, `.claude/` |
| Local sandbox | Seatbelt / Landlock+seccomp, network deny by default | bubblewrap on Linux, opt-in, no Windows, network filter "unstable" |
| Approvals | Auto-review classifier, allowlist, run everything | allow / ask / deny, Bypass Permissions mode |
| Own models | Tab, Composer 2.5 (Kimi base), Grok with SpaceXAI | SWE-2 (Kimi K3 base), SWE-2 Flash (Inkling base), SWE-grep |
| Model policy | Many vendors, but cheap tiers Grok-only | "independent agent lab," mixes vendors per task |
| Protocols | ACP server (CLI), MCP, hooks compatible with Claude Code | ACP host (Desktop) and ACP agent (CLI), MCP |
| Own SDLC stack | Origin hosting, Bugbot, Security Review, Rollouts, Agent SDK | Devin Review, Devin Security, Auto-Triage, DeepWiki |

## Part D: Notes for a bank audience [O]

- [O] Neither tool is approved for the audience; these are reference designs. The two transferable patterns: one writer with read-only helpers, and a clean-context reviewer. Both vendors arrived there independently.
- [O] "Self-hosted" does not mean "on-prem inference" at Cursor: tool outputs, possibly containing code, go back to Cursor's cloud. Cognition sells VPC and dedicated deployments at Enterprise tier; we did not fetch their data-flow docs.
- [O] Windows engineers: Cursor documents no Windows terminal sandbox; Devin CLI states none exists.
- [O] The Oct 29 extension-marketplace compromise is a concrete example for supply-chain risk in AI editors that pull from a VS Code-style marketplace.
- [O] Both companies publish their own benchmarks (CursorBench, FrontierCode). Treat their numbers as vendor claims.

## Open questions

- Has Cursor's from-scratch SpaceXAI model shipped, and under what name? Cursor's models page lists none called Composer 3; Grok 4.7 is described by x.ai as "a new, larger base model" without saying from scratch.
- Cursor's 2026 edit tool format (still a separate apply model, or str_replace / patch style?) is undocumented.
- Cognition's edit format and macOS sandbox mechanism for Devin CLI are undocumented.
- Whether Devin Desktop's RAG "Context Awareness" index is still active by default, given Cognition's stance against embeddings.
- How Cursor Projects decides a task is done; not stated.

## Verification pass (2026-11-04)

Method: re-fetched every cited page below as raw HTML with curl and string-matched each quote after decoding HTML entities and curly apostrophes; used WebFetch for dates, authors and numbers. Quotes that matched raw text are [P]; quotes seen only through WebFetch are [P*].

**Headline claims checked (12):**

1. SpaceX acquisition closed Aug 14, 2026: confirmed ("officially been acquired by SpaceX"; "completes the acquisition process that started in April"). The Cursor post gives no price; $60B all-stock, expected Q3 close and the April option come from BNN Bloomberg (Jun 16, 2026) [S].
2. Embeddings indexing turned down for grep-based retrieval, July 2026: confirmed on the forum; all quoted posters carry the staff flag in the thread JSON. Fixed attribution: "rapidly no longer helping" is maximep (Jul 21), not Colin; the `.git/cursor/`, half-size and ripgrep-fallback details are Colin (Jul 28). Fixed "trigram": Cursor's own post says "Sparse N-grams."
3. System prompt trimmed about 66%, token cost down 7% "without reducing agent quality": confirmed. Partly refuted: the page does not say the prompt trim was validated by A/B tests on live traffic (A/B tests are described for tool-loading configs), and two phrases presented as quotes ("long lists of prohibitions and emphasis markers", "evals often focus on hard problems that don't match real traffic") are not on the page. Replaced with page wording.
4. 35% of internally merged PRs created by agents in cloud VMs (Feb 26, 2026, Michael Truell): confirmed verbatim.
5. Self-summarization reduces compaction error by 50% vs a tuned prompt baseline: confirmed verbatim ("a highly tuned prompt-based compaction baseline"; Federico Cassano and Sasha Rush, Mar 17, 2026).
6. Projects coordinator that doesn't write code, "thousands of subagents": confirmed verbatim (Sep 10, 2026; Alexi Robbins and Fredrika Lindh). Fixed the trigger quote; "grow with the Project" not found.
7. Composer 2.5 on Kimi K2.5; larger from-scratch model with SpaceXAI at 10x compute: confirmed. Fixed wording: "significantly larger," not "much larger."
8. Cursor sandbox (Seatbelt; Landlock + seccomp, kernel 6.2+), network blocked by default, "The classifier can make mistakes": confirmed verbatim.
9. Walden Yan follow-up (Apr 22, 2026), writes single-threaded and swarms "mostly a distraction": confirmed verbatim; the swarm sentence opens with "We think".
10. Windsurf became Devin Desktop Jun 2, 2026, "fully backwards-compatible with Windsurf": confirmed verbatim (Scott Wu and Jeff Wang). Note: the launch post does not mention Devin Local or Cascade.
11. Devin Fusion 68.1 at $9.01 vs Claude Code (Opus 5.5) at $13.04, about 31% cheaper: confirmed on the local-fusion chart (Artificial Analysis Coding Agent Index v1.5, chart updated 10/19/2026). Context worth keeping: Claude Code (Opus 5.5) scored 66 on that chart, and Claude Code with Sonnet 5.5 scored 68.4, above Fusion. Page has no named author.
12. Devin CLI sandbox: bubblewrap on Linux, not supported on Windows, network filtering "currently unstable": confirmed verbatim.

**Other claims spot-checked:** Truell "factory" and "human role" quotes; Truell and Asif IDE quote; Wilson Lin quotes (all six); Composer (1) quotes (all five); semsearch 12.5% and "currently necessary" quotes; fast-regex-search quotes; instant-apply quotes; Agent SDK GA and quote; Walden Yan 2025 quotes (all five); cloud-agents quotes (all five); SWE-grep numbers and embeddings quote; Series E ($2B+ at $48B, customers, three quotes); $1B run rate; 44 to 350 headcount; SWE-1.7, SWE-2, SWE-2 Flash numbers; Cursor pricing tiers; self-hosted machines quotes; Oct 29 extension incident; Devin Security, Corridor, testing-development, Devin 2.2, managed Devins, Sonnet 4.5 lessons, Jack Cable quotes; Devin Local docs quotes; Grok 4.7 x.ai post.

**Corrected (beyond the headline list):**
- Read-tool change: "with no reduction in quality," not "with no quality loss."
- Cursor 3 LSP quote: "go to definition in the editor with full LSPs."
- Agent SDK: folder names (`instructions.md`, `tools/`, etc.) and `agent-sdk eval` / `agent-sdk github replay` are not in the GA post; now [E].
- Grok row: the "with SpaceXAI" label is not on Cursor's models page (it says "Cursor's own models"); the x.ai page is branded "SpaceXSI" (SpaceX Super Intelligence LLC), not SpaceXAI.
- Managed Devins "through an internal MCP": not on the page.
- Fusion cache-miss quote: "which would trigger a cache miss anyway" (devin-fusion post).
- "When the judgment is the deliverable, delegating it backfires": not on the Joon Hee Lee post; struck.
- SWE-1.7 and Sonnet 4.5 compaction quotes replaced with page wording.
- SWE-2 Flash: "a fully American coding model"; weight-withholding wording replaced.
- SWE-2 rollout and sandbox Strict-mode quotes replaced with page wording.
- 44 to 350 headcount and the Windsurf date come from the one-year-of-building-together post, not 1b-run-rate.

**Could not verify / left as is:**
- SpaceX deal price and terms: secondary only (BNN Bloomberg).
- Composer 2 base disclosure and the Aman Sanger "It was a miss" quote: secondary only (VentureBeat), not re-checked.
- 1.5T params / 100k GPUs for the from-scratch model, and Composer 3: aggregator-only; still [R]/[S].
- Grok 4.7 "to natively understand the Grok Bot harness": seen through the summariser only; raw match failed (likely split by markup). [P*].
- Changelog-only items (dates of side chats, `/goal`, Builds, Origin, Rollouts, iOS remote control, etc.) and Devin pricing were not re-fetched in this pass.
