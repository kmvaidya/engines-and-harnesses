---
url: https://github.com/SWE-agent/mini-swe-agent, https://mini-swe-agent.com/latest/advanced/v2_migration/, https://arxiv.org/pdf/2603.05344, https://picrew.github.io/LLM-Harness/main.pdf, https://infoq.com/news/2026/04/anthropic-three-agent-harness-ai/, https://codex.danielvaughan.com/2026/04/17/agents-sdk-harness-portable-sandbox-manifests-codex-cli/, https://github.com/ai-boost/awesome-harness-engineering, https://epoch.ai/benchmarks/swe-bench-verified, https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents, https://www.anthropic.com/engineering/harness-design-long-running-apps, https://www.anthropic.com/engineering/managed-agents, https://developers.openai.com/api/docs/guides/agents/sandboxes.md, https://openai.github.io/openai-agents-python/sandbox/, https://learn.chatgpt.com/docs/mcp-server.md, https://learn.chatgpt.com/docs/agent-approvals-security.md, https://github.com/Gloriaameng/Awesome-Agent-Harness, https://blog.modelcontextprotocol.io/posts/2026-03-16-tool-annotations/, https://blog.modelcontextprotocol.io/posts/2026-07-28/, https://modelcontextprotocol.io/specification/2026-07-28/changelog, https://langchain.com/blog/improving-deep-agents-with-harness-engineering, https://stencil.so/blog/the-harness-problem, https://techcommunity.microsoft.com/blog/appsonazureblog/the-agent-that-investigates-itself/4500073, https://github.com/statewright/statewright, https://www.preprints.org/manuscript/202604.0428/v3
fetched: 2026-09-30
---

# Harness reference designs: what a harness is made of, and designs to study

Round 2 file. Tags: **[V]** 3-agent adversarial check passed, **[S]** hand
spot-check, **[P]** confirmed against the primary source on 2026-09-30,
**[E]** extracted with quote but not cross-checked, **[R]** refuted.

## 1. Two published ways to divide a harness into parts

- **ETCLOVG** [P]. "Agent Harness Engineering: A Survey" (Li, Xiao, Zhang,
  Liu et al.; CMU, Stanford, Yale, Amazon and others), 71-page PDF at
  picrew.github.io/LLM-Harness/main.pdf. No printed date (PDF metadata says
  Jul 20, 2026); "the metadata snapshot reported in this version was frozen
  on May 08, 2026." No arXiv version found; secondary sites say it is under
  review at TMLR. Seven layers: **E**xecution environment, **T**ool
  interface, **C**ontext management, **L**ifecycle/Orchestration,
  **O**bservability, **V**erification, **G**overnance. "We map more than 170
  open-source projects" (an earlier version said 148+).
- **Meng et al. (2026)** [P]. "Agent Harness for Large Language Model
  Agents: A Survey", Preprints.org (not peer reviewed, not on arXiv). Cite
  **v3**: DOI 10.20944/preprints202604.0428.v3, posted Apr 28, 2026, 11
  authors (Qianyu Meng, Yanan Wang, Liyi Chen, Yihang Li, Wei Wu, Wenyuan
  Jiang, Qimeng Wang, Chengqiang Lu, Yan Gao, Yi Wu, Yao Hu). v1 and v2 (Apr
  7 and 9) had 9 authors. The v3 abstract: "A formal definition of the agent
  harness as a six-component tuple H = (E,T,C,S,L,V), i.e., execution loop,
  tool registry, context manager, state store, lifecycle hooks, and
  evaluation interface." It surveys 23 systems. Caveat: the v2 abstract
  lists a different six ("Execution environment, Tool integration, Context
  management, Scope negotiation, Loop management, Verification"), though the
  v2 body uses the same tuple. The ETCLOVG survey cites the tuple.
- The two lists mostly agree. ETCLOVG adds observability and governance,
  which are the layers a bank will be asked about.

## 2. mini-swe-agent: the minimal baseline

- [V] Core agent class is about 100 lines of Python (whole package about
  9,000). README: "Scores >74% on the SWE-bench verified benchmark."
- [V] Authors' reason it works: "As LMs have become more capable, a lot of
  this is not needed at all to build a useful agent." The "this" is the
  original SWE-agent's custom agent-computer interface, tool sets and history
  processors. They still recommend full SWE-agent for experimenting with those.
- [V] Independent-ish numbers: Simon Willison (2026-02-19) reports bash-only
  leaderboard runs through mini-swe-agent, run by the SWE-bench team: Opus 4.5
  76.8%, Gemini 3 Flash 75.8%. The >74% figure dates from Feb 2026 runs; no
  rerun on the newest models was found.
- **Correction to a common description [R, 0-3]:** it is wrong to say
  mini-swe-agent "does not use the model's tool-calling interface." **v2 uses
  native tool calling by default** (a `bash` tool); regex text parsing is now
  the legacy option. What still holds: bash is the only tool, history is
  linear, and each action runs as an independent `subprocess.run` with no
  persistent shell.
- [P] README: "Supports local environments, docker/podman,
  singularity/apptainer, bublewrap [sic], contree, and more". Self-reported
  users: "Meta, NVIDIA, Essential AI, IBM, Nebius, Anyscale, Princeton
  University, Stanford University". Scale's SWE-bench Pro board now runs its
  top entries with mini-swe-agent (`round2-evals-and-benchmarks.md` §3).
- Round 1 (`track3-benchmarks.md`) said "bash as its only tool". Still true;
  add the v2 tool-calling note if a slide describes internals.

## 3. Epoch AI's evaluation harness: another minimal reference [P]

- "a simple loop where models can take an individual action (e.g. reasoning
  and tool call), then see any output." Three tools: `bash`, Inspect's
  Anthropic-style `text_editor`, and an OpenAI-style `apply_patch`.
- Budget: "We limit model token usage to 2M uncached read/write tokens
  (including reasoning), and 20M cached token reads." Limits are checked
  "after each turn"; at the limit the model is "forced to submit its current
  working state". So the limits apply to each task attempt. Budget is a
  harness setting that moves scores.
- See `round2-evals-and-benchmarks.md` §3 for the Feb 2026 v2.0 upgrade.

## 4. OpenDev (arXiv 2603.05344): a fuller reference design [V]

"Building Effective AI Coding Agents for the Terminal: Scaffolding, Harness,
Context Engineering, and Lessons Learned". Single-author preprint (Nghi D. Q.
Bui; v1 Mar 5, v3 Mar 13 2026 [P]) describing the author's own open-source,
MIT-licensed Rust terminal agent (github.com/opendev-to/opendev).
**Not peer reviewed, and it reports no benchmark scores** [P]: "This paper
documents architectural decisions and design rationale but lacks systematic
quantitative evaluation." Use it as a design catalogue, not as evidence of
what works.

- **Planning separated from execution.** The main agent spawns a Planner
  subagent with read-only tools. "Write operations are excluded from the
  subagent's tool schema entirely: the LLM never sees tool definitions it
  cannot use." The user approves or revises the plan before execution.
- **Five safety layers:**
  1. prompt-level policy
  2. schema-level tool whitelists (plan mode, per-subagent `allowed_tools`,
     MCP discovery gating)
  3. runtime approval: Manual, Semi-Auto or Auto, with persistent permissions
  4. tool-level validation: dangerous-pattern blocklist, stale-read detection,
     output truncation, timeouts
  5. lifecycle hooks: "Pre-tool blocking (exit code 2), argument mutation,
     JSON stdin protocol". The hook protocol closely resembles Claude Code's.
- **Context pressure as the central constraint** (§3.1 title). "apply
  progressively aggressive compaction as token usage grows"; MCP tools found
  lazily by keyword search; project memory kept across sessions. Self-reported
  figures [P]: "tool outputs (file contents, command results, search hits)
  consume 70–80% of the context in a typical session"; MCP schemas consumed
  "up to 40% of the context before the first user message. Lazy discovery
  reduced baseline overhead to nearly zero (<5%)".
- [P] **Instruction fade-out** (the paper's term): "event-driven system
  reminders that counteract instruction fade-out in long-running sessions by
  injecting targeted guidance at the point of decision rather than relying
  solely on the initial system prompt".
- [P] "Five model roles with fallback chains", "each independently bound to a
  user-configured LLM": Action (primary; "Normal" in the code), Thinking,
  Critique, Vision (VLM) and Compact (summarises during compaction). Each
  falls back towards Action. Switching provider is a config change.
- Minor inconsistency in the paper: mutated hook arguments are called
  `tool_input` in one place and `updatedInput` in another.

## 5. Anthropic's three-agent harness for long-running app development [P]

Primary: "Harness design for long-running application development"
(anthropic.com/engineering/harness-design-long-running-apps, Mar 24, 2026),
written by Prithvi Rajasekaran, "a member of our Labs team". Checked on
2026-09-30 against the raw page. Round 2 first built this section from InfoQ
coverage (Apr 4, 2026), and three of its points were wrong; they are corrected
below.

- **Planner, generator, evaluator.** The first experiment (frontend design)
  used only a generator and an evaluator. The planner was added for the
  full-stack harness.
- **Why an evaluator.** "When asked to evaluate work they've produced, agents
  tend to respond by confidently praising the work—even when, to a human
  observer, the quality is obviously mediocre. This problem is particularly
  pronounced for subjective tasks like design." The evaluator was calibrated
  "using few-shot examples with detailed score breakdowns" against four
  grading criteria: design quality, originality, craft, functionality.
  [R] The InfoQ wording "Agents often overrate their results" is not in the
  post; do not quote it as Anthropic's.
- "Separating the agent doing the work from the agent judging it proves to be
  a strong lever to address this issue." This is the author's prose, not a
  spoken quote from an "engineering lead" as InfoQ framed it. The next
  sentence matters: "The separation doesn't immediately eliminate that
  leniency on its own."
- **Context resets vs compaction.** "Context anxiety" is in the post: models
  "begin wrapping up work prematurely as they approach what they believe is
  their context limit." Sonnet 4.5 showed it "strongly enough that compaction
  alone wasn't sufficient ... so context resets became essential", because
  compaction "doesn't give the agent a clean slate". **This post's harness did
  not use resets:** "Opus 4.5 largely removed that behavior on its own, so I
  was able to drop context resets from this harness entirely", relying on the
  Claude Agent SDK's automatic compaction. [R] The InfoQ line that compaction
  "can make models cautious about approaching context limits" is not in the
  post.
- **Playwright MCP.** The evaluator "used the Playwright MCP to click through
  the running application the way a user would, testing UI features, API
  endpoints, and database states."
- **Run sizes.** "5 to 15 iterations per generation" and "up to four hours"
  describe the frontend-design loop only. Full-stack: a retro game maker on
  Opus 4.5 took 6 hours and $200, against 20 minutes and $9 for a single
  agent. A later version on Opus 4.6 built a DAW app in 3 hr 50 min for
  $124.70. "4-6 hours" is not in the primary.
- **Resets became dead weight.** A second Anthropic post, "Scaling Managed
  Agents: Decoupling the brain from the hands" (anthropic.com/engineering/managed-agents,
  Apr 8, 2026), says the same: "when we used the same harness on Claude Opus
  4.5, we found that the behavior was gone", and calls the resets "dead
  weight". This is the thin-harness thesis from a primary source (see
  `track2-thin-harness-evidence.md`).
- [R] **The survey in §1 misreads this post.** It says resets "became
  dispensable for a stronger model, and removing them reduced cost without
  degrading quality", and elsewhere that moving from Opus 4.5 to 4.6 "removed
  the sprint construct and context resets entirely, reducing cost from $200
  to $125 while maintaining output quality." The Anthropic post says resets
  were already gone at Opus 4.5; the 4.6 change removed the sprint construct.
  The $200 and $124.70 runs built different apps on different models, and
  neither Anthropic post measures quality before and after removing resets.
  Do not repeat the survey's version.

## 6. OpenAI Agents SDK sandbox harness and Codex CLI [P]

Round 2 first built this from a blog (codex.danielvaughan.com). Now checked
against OpenAI's post "The next evolution of the Agents SDK" (openai.com, read
through a reader proxy because openai.com refused direct fetches), the sandbox
guide (developers.openai.com/api/docs/guides/agents/sandboxes.md), the SDK
docs (openai.github.io/openai-agents-python/sandbox/) and the Codex docs.

- **Released Apr 15, 2026**, not Apr 16 (the press date): openai-agents-python
  v0.14.0 "adds **Sandbox Agents**, a beta SDK surface". TypeScript followed
  May 6. OpenAI's wording on the split: "Separating harness and compute helps
  keep credentials out of environments where model-generated code executes."
  The guide: the application keeps "sensitive control plane work in trusted
  infrastructure while the sandbox stays focused on provider-specific
  execution." [R] The blog's quote ("The harness runs in trusted
  infrastructure ... Credentials remain outside ...") is not OpenAI's text.
- **Sandbox clients:** Unix-local, Docker, Blaxel, Cloudflare, Daytona, E2B,
  Modal, Runloop, Vercel. Caution: "On Linux, this backend [Unix-local] adds
  no OS-level confinement"; on macOS it uses sandbox-exec without network
  isolation. Unix-local is for development only.
- **Portable manifests:** "Manifest entry paths are workspace-relative. They
  cannot be absolute paths or escape the workspace with .., which keeps the
  workspace contract portable across local, Docker, and hosted clients."
- **Snapshot and rehydrate:** "losing a sandbox container does not mean
  losing the run ... the Agents SDK can restore the agent's state in a fresh
  container and continue from the last checkpoint".
- **Capabilities:** Shell, Filesystem, Skills, Memory, Compaction.
  `Capabilities.default()` includes Filesystem, Shell and Compaction. Memory
  "Requires Shell". Its layout is `memories/` with `MEMORY.md`,
  `memory_summary.md`, `raw_memories.md` (intermediate, consolidated into the
  other two) and `rollout_summaries/`.
- [R] **Codex CLI as an MCP tool no longer works.** `codex mcp-server` (tools
  `codex` and `codex-reply`) was removed in Codex rust-v0.154.0 (Sep 9, 2026):
  "The deprecated `codex mcp-server` entry point is no longer available." The
  Codex docs say the previous "Agents SDK examples on this page are no longer
  supported." The replacement, the Codex app server, is "experimental and
  isn't supported for production workloads".
- **Codex CLI's OS sandbox:** "macOS uses Seatbelt policies and runs commands
  using `sandbox-exec`"; "Linux uses `bwrap` plus `seccomp` by default" (since
  0.115). Windows natively uses an `elevated` sandbox (dedicated
  lower-privilege users plus firewall rules), falling back to an
  `unelevated` sandbox with "a restricted Windows token". WSL2 uses the Linux
  sandbox.
- **Layering:** no OpenAI doc pairs an SDK sandbox outside with Codex CLI
  inside; that was the blogger's idea, and the MCP bridge it needed is gone.
  OpenAI's own layering advice is Codex inside a Dev Container, letting
  "Docker provide the outer isolation boundary" with bubblewrap inside. If the
  container blocks namespaces or seccomp, the docs say to run
  `--sandbox danger-full-access` inside it, which drops the inner layer.

## 7. Context engineering: the principles behind §4-§6 [V]

Not new (Anthropic, Sep 29 2025; already in `track2-anthropic-context-engineering.md`).
Restated here because every design above implements it.

- Context rot: "as the number of tokens in the context window increases, the
  model's ability to accurately recall information decreases." Chroma's
  independent study of 18 models agrees; it is a gradient, not a cliff, and
  newer models degrade less steeply.
- Just-in-time retrieval through lightweight references and grep/glob/head/tail.
- For long tasks: compaction (tool-result clearing is among the lightest
  forms), structured notes (NOTES.md or a memory tool), and subagents that
  spend tens of thousands of tokens but return "often 1,000-2,000 tokens."
  That figure is illustrative, not measured.
- [P] Tool design: "If a human engineer can't definitively say which tool
  should be used in a given situation, an AI agent can't be expected to do
  better."

## 8. Practitioner evidence that harness changes move results [P]

Each row is now checked against the builder's own post. All are still
self-reported by the builder: good for illustration, weak as proof.

| Change, model held fixed | Result | Primary source |
|---|---|---|
| LangChain DeepAgents, gpt-5.2-codex: system prompt built around plan, build, verify, fix; middleware for self-verification (PreCompletionChecklist), context injection and loop detection. "We only tweaked the harness and kept the model fixed" | Terminal-Bench 2.0: 52.8 to 66.5 (+13.7); "just outside the Top 30" to Top 5 | Vivek Trivedy, langchain.com/blog/improving-deep-agents-with-harness-engineering, Feb 17, 2026 |
| New "hashline" edit format vs patch and replace; "Sixteen models, three edit tools" | "Grok Code Fast 1 went from 6.7% to 68.3%, a tenfold improvement" | Can Bölük, "We improved 15 LLMs at coding in one afternoon. Only the harness changed." (blog.can.ac, now stencil.so/blog/the-harness-problem), Feb 12, 2026 |
| Azure SRE Agent: agent's world "materialized ... as a repo-like workspace", used via read_file, grep, find, shell | "Intent Met" on novel incidents "rose from 45% to 75%" | Microsoft Tech Community, "The Agent that investigates itself", Mar 10, 2026 |
| statewright: state machine limits tools per phase (planning: Read/Grep/Glob; implementing: Read/Edit/Write; testing: Bash for tests only) | gpt-oss:20b and gemma4:31b went "from 2 of 10 attempts passing to 10 of 10" on a 5-task SWE-bench subset | github.com/statewright/statewright README; tiny sample |

Corrections from the primary pass:

- [R] Azure: "100+ bespoke tools replaced by files" merges two posts. The
  "100+ tools" is from an earlier post ("Context Engineering Lessons from
  Building Azure SRE Agent", Dec 26, 2025), where the fix was "5 core tools
  and a handful of generalists" using az and kubectl, not files. The 45% to
  75% result is from the Mar 2026 post and does not mention 100+ tools.
- Bölük tested 16 models, not 15, despite the title.
- The LangChain result is a single benchmark run by the vendor of the
  harness.

## 9. Two pointers for tool and protocol design [P]

- **MCP tool annotations.** "Tool Annotations as Risk Vocabulary: What Hints
  Can and Can't Do" (blog.modelcontextprotocol.io/posts/2026-03-16-tool-annotations/,
  Mar 16, 2026; Ola Hungerford, Sam Morrow of GitHub, Luca Chang of AWS).
  Four hints: `readOnlyHint`, `destructiveHint`, `idempotentHint`,
  `openWorldHint`, shipped in the 2025-03-26 spec. A harness can feed them
  into permission decisions: "A tool marked `readOnlyHint: true` from a
  trusted server might be auto-approved, while `destructiveHint: true` gets a
  confirmation step." The post also says "a tool's risk depends on what else
  is in the session", citing the lethal trifecta.
  **Trust limit:** the spec (2025-06-18, server/tools) says "clients **MUST**
  consider tool annotations to be untrusted unless they come from trusted
  servers." A malicious server can label a destructive tool read-only.
- **MCP spec 2026-07-28 is final**, not a release candidate. The RC was
  locked on May 21, 2026; the final shipped Jul 28, 2026
  (blog.modelcontextprotocol.io/posts/2026-07-28/; changelog at
  modelcontextprotocol.io/specification/2026-07-28/changelog). Changes:
  stateless core ("remove the `initialize`/`notifications/initialized`
  handshake", SEP-2575); protocol-level sessions and the `Mcp-Session-Id`
  header removed (SEP-2567); extensions with reverse-DNS IDs in `ext-*`
  repositories, the two official ones being Tasks and MCP Apps; "a minimum
  twelve-month deprecation window" (SEP-2596). It also deprecates Roots,
  Sampling and Logging, and Dynamic Client Registration in favour of Client
  ID Metadata Documents.
