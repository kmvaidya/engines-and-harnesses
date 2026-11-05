# Research index

Round 1: 38 files, all fetched **2026-08-12**. Round 2: 6 files fetched
**2026-09-30** (see the end of this page). Every file opens with frontmatter
carrying its source URL(s) and fetch date. The deck (`../index.html`) is built from these files,
not from model memory; where a slide states a perishable fact, this directory is
the receipt.

## Track 1 — GitHub Copilot's customization surface (14 files)

| File | What it covers |
|---|---|
| [track1-repo-custom-instructions.md](track1-repo-custom-instructions.md) | `.github/copilot-instructions.md`; personal/repo/org instruction tiers; full precedence order; per-surface support matrix |
| [track1-path-specific-instructions.md](track1-path-specific-instructions.md) | `*.instructions.md`, `applyTo` glob syntax (comma-separated in one string), new `excludeAgent` key |
| [track1-agents-md.md](track1-agents-md.md) | AGENTS.md support incl. nesting; CLAUDE.md/GEMINI.md honored as equivalents; precedence vs copilot-instructions.md |
| [track1-prompt-files.md](track1-prompt-files.md) | `*.prompt.md` frontmatter (`agent:` replaced `mode:`), slash invocation, `${input:}` variables, migration toward skills |
| [track1-custom-agents.md](track1-custom-agents.md) | `.agent.md` (renamed from chat modes), tools/model-fallback/subagents/handoffs/`target:` |
| [track1-agent-skills.md](track1-agent-skills.md) | SKILL.md format, three-level progressive disclosure, open Agent Skills standard, `.claude/skills/` read natively |
| [track1-hooks.md](track1-hooks.md) | Full lifecycle-hook system: 14 events, allow/deny/modifiedArgs, exit-code semantics, cloud-agent subset |
| [track1-mcp.md](track1-mcp.md) | `.vscode/mcp.json`, repo-settings `mcpServers`, sandboxing, cloud-agent + code-review MCP, default servers |
| [track1-coding-agent.md](track1-coding-agent.md) | Cloud agent (renamed from coding agent): issue→PR flow, Actions sandbox, `copilot-setup-steps.yml`, firewall, 59-min cap |
| [track1-code-review.md](track1-code-review.md) | Code review as configurable agent: which instruction files it reads, effort levels, credit costs |
| [track1-memory-spaces.md](track1-memory-spaces.md) | Copilot Memory (cited facts, 28-day expiry, cross-feature) and Spaces (curated context bundles) |
| [track1-models.md](track1-models.md) | Aug-2026 model list, AI credits (premium requests are legacy), plans incl. new Max/Student, auto model selection |
| [track1-context.md](track1-context.md) | What Copilot sends: #codebase, semantic/remote indexing, 1M-token context tier |
| [track1-other-surfaces.md](track1-other-surfaces.md) | Agentic Workflows (`engine: copilot\|claude\|codex\|gemini`), CLI stack, plugins, SDK, governance |

## Track 2 — Vendor AI-engineering doctrine (19 files)

Anthropic per-source: [engineering-index](track2-anthropic-engineering-index.md) ·
[building-effective-agents](track2-anthropic-building-effective-agents.md) ·
[context-engineering](track2-anthropic-context-engineering.md) ·
[writing-tools-for-agents](track2-anthropic-writing-tools-for-agents.md) ·
[multi-agent-research](track2-anthropic-multi-agent-research.md) ·
[code-execution-mcp](track2-anthropic-code-execution-mcp.md) ·
[long-running-harnesses](track2-anthropic-long-running-harnesses.md) ·
[prompting-best-practices](track2-anthropic-prompting-best-practices.md) ·
[prompting-claude-fable-5](track2-anthropic-prompting-claude-fable-5.md) ·
[prompting-claude-opus-5](track2-anthropic-prompting-claude-opus-5.md) ·
[context-management-memory](track2-anthropic-context-management-memory.md) ·
[new-rules-context-engineering](track2-anthropic-new-rules-context-engineering.md) (the 80% post).

OpenAI per-source: [gpt41-prompting-guide](track2-openai-gpt41-prompting-guide.md) ·
[gpt5-prompting-guides](track2-openai-gpt5-prompting-guides.md) ·
[reasoning-best-practices](track2-openai-reasoning-best-practices.md) ·
[practical-guide-building-agents](track2-openai-practical-guide-building-agents.md).

Syntheses (the deck leans on these):
- [track2-generation-shift.md](track2-generation-shift.md) — 2023 instruct doctrine vs 2026 reasoning doctrine, row by row, every claim URL-traced. Source for Act 7's shift table.
- [track2-vendor-disagreements.md](track2-vendor-disagreements.md) — where the labs genuinely split (multi-agent stance, migration mechanics, XML vs markdown) and where they boringly agree.
- [track2-thin-harness-evidence.md](track2-thin-harness-evidence.md) — the 80% claim, verified to its primary source, with caveats.

## Track 3 — Benchmarks, FLOPs, Papyan, demos (5 files)

- [track3-benchmarks.md](track3-benchmarks.md) — SWE-bench Verified state of play, Terminal-Bench 2.1 leaderboard, Aider polyglot (stale), LiveCodeBench, METR time horizons; scaffold-delta evidence table.
- [track3-benchmark-critiques.md](track3-benchmark-critiques.md) — contamination, SWE-Bench Illusion, task-realism critiques, vendor self-reporting, saturation.
- [track3-flops.md](track3-flops.md) — 2N/6N rules (Kaplan, Epoch), Llama 3.1 405B official figures, Cray-1/H100/human comparisons with arithmetic shown.
- [track3-papyan-course.md](track3-papyan-course.md) — MAT1510 found; syllabus arc 2021→2025; all public slide links; correction: it links no interactive demos.
- [track3-demo-embeds.md](track3-demo-embeds.md) — iframe embeddability probe of every demo; all core demos embed.

## Surprises worth knowing (what moved since 2025)

1. **The 80% claim is real and citable** — Anthropic's own July 2026 blog post, exact
   wording "no measurable loss *on our coding evaluations*"; older models still ship
   the fat prompt. The deck's thesis has a primary source.
2. **Premium requests are dead** — Copilot billing became per-token AI credits
   (June 2026); most 2025 cost advice is obsolete.
3. **Copilot absorbed Claude Code's harness design** — hooks, Agent Skills,
   `.claude/skills/`, `CLAUDE.md`, and `.claude/settings.json` all work natively.
4. **"Chat modes" → custom agents, "coding agent" → cloud agent** — 2025 terminology
   is stale across the board; VS Code's docs moved to an "agent customization" section.
5. **Copilot Memory exists** — machine-written, citation-backed, 28-day-expiring
   memory shared across agent surfaces. The "memory engineering" leg is now real product.
6. **All five core demos embed** — no X-Frame-Options anywhere in the core set;
   only Colab, Substack, and YouTube `/watch` refuse framing.
7. **SWE-bench Verified is finished as a signal** — ~96% vendor-reported top scores,
   its co-creator's evals team walked away, and scaffold choice swings scores by
   10–25 points — which is the deck's whole argument wearing a lab coat.
8. **Papyan's MAT1510 links no demos** — the brief assumed otherwise; its actual
   gift is the 2021→2025 syllabus drift and the theory framing.

---

# Round 2 — 2026-09-30

Gathered for a "Build-Your-Own-Harness" series for engineers at a bank. Round 1
files are left unchanged as the Aug 12 record; round 2 files record what is new,
what changed, and new topics (harness design, agent security).

Every claim in a round-2 file carries a tag:

- **[V]** passed a 3-agent adversarial check (2 of 3 refutes needed to kill)
- **[S]** spot-checked by hand against the live page on 2026-09-30
- **[P]** confirmed against the primary source (the publisher's own page,
  paper, repo or changelog) on 2026-09-30, with that source's URL recorded
- **[E]** extracted with a quote from the named source, not cross-checked
- **[R]** refuted; recorded so nobody reuses it

**Primary-source pass (2026-09-30, same day):** every [E] claim and every
claim built on a secondary source was checked against its primary source.
Most held; the ones that did not are now marked [R] next to the corrected
version. One [E] remains (a blog's general "10-20 points" claim, backed by the
primary examples next to it). The biggest corrections:

- OWASP Agentic Top 10: three of six incident-to-risk mappings came from the
  launch blog and differ from the full PDF.
- FINOS v2.0: the four "new risks" were blog bullets; the framework's six
  agentic risks (AIR-SEC-024 to 029) are now listed.
- SandboxEscapeBench: "15-35%" came from the survey; the paper's top models
  escape about half the time (GPT-5 0.50, Opus 0.49).
- Anthropic's three-agent harness: it dropped context resets for Opus 4.5;
  the InfoQ and survey versions said otherwise.
- Codex CLI's MCP server mode, which the Agents SDK pairing relied on, was
  removed on Sep 9, 2026.
- MCP spec 2026-07-28 is final, not a release candidate.
- MCP allowlists in enterprise managed settings went GA on Aug 6, 2026, but
  not for the cloud agent.

| File | What it covers |
|---|---|
| [round2-copilot-changes.md](round2-copilot-changes.md) | Content exclusions in app/CLI, local sandboxing (preview), cloud-agent firewall limits, Sep 1 / Oct 2 / Oct 19 model retirements, billing, data residency; §9 instructions, AGENTS.md, prompt files, custom agents; §10 enterprise-managed permissions, skills, hooks, Memory, CLI, SDK, plugins |
| [round2-agent-permission-models.md](round2-agent-permission-models.md) | Approval modes, sandboxing, admin lock-down and secrets handling compared across Claude Agent SDK/Claude Code, Codex CLI, OpenAI Agents SDK, Copilot cloud agent and CLI; what a bank harness should copy |
| [round2-harness-reference-designs.md](round2-harness-reference-designs.md) | Two ways to divide a harness into parts (ETCLOVG, Meng et al.), mini-swe-agent v2, Epoch's harness, OpenDev, Anthropic's three-agent harness, OpenAI Agents SDK sandbox harness, practitioner harness deltas, MCP annotations and the final 2026-07-28 spec |
| [round2-frontier-model-guidance.md](round2-frontier-model-guidance.md) | Claude Fable 5 harness guidance (long turns, verifier subagents, no token countdowns), the GPT-6 family and its async tools / mid-turn steering, Gemini 3.x guidance (thinking levels, remove temperature) |
| [round2-agent-security-governance.md](round2-agent-security-governance.md) | OWASP Agentic Top 10, FINOS AI Governance Framework v2.0, lethal trifecta, sandbox escapes, Copilot Enterprise AI Controls and MCP controls |
| [round2-vscode-copilot-setup.md](round2-vscode-copilot-setup.md) | (Oct 1) VS Code session targets, `/init` per surface, agents and permission levels, exact approval settings, skills, how to see what loaded, JetBrains differences. Source for the Build Your Own Harness deck's setup slides |
| [round2-evals-and-benchmarks.md](round2-evals-and-benchmarks.md) | Score = model + harness (CORE-Bench 42% to 95%), first eval suite advice, pass^k, Epoch v2.0 and SEAL results; §6 independent results for the GPT-6 / Fable 5 generation |

## Round 3 — 2026-10-01 (Build Your Own Harness, Part 1)

Same tags as round 2, plus **[O]** for our own recommendation. Gathered for
the Part 1 deck in `../build-your-own-harness/`.

| File | What it covers |
|---|---|
| [round3-framing-taxonomy-changes.md](round3-framing-taxonomy-changes.md) | Source of the knowns/unknowns framing (Thariq Shihipar, claude.com, Jul 6 2026); technical debt taxonomies and seven recommended auditor categories; dated Copilot changes Aug 13 to Oct 1 |
| [round3-hooks-context-memory.md](round3-hooks-context-memory.md) | Hook formats and events for Local vs Copilot sessions, blocking `git push` and protected paths (tested scripts), what hooks can't see, PostToolUse/SessionStart/Stop uses, what VS Code loads before your prompt, the two memory systems |
| [round3-customizations-and-automation.md](round3-customizations-and-automation.md) | Prompt files vs skills vs custom agents, example skill/prompt/agent files, running agents in parallel, cloud agent automations and Agentic Workflows, what goes in instructions, AGENTS.md vs copilot-instructions.md, personal instruction files |

## Round 4 — 2026-11-04 (writing that doesn't read as AI)

Same tags as round 3, plus **[P\*]** for a primary source whose quote came
back through a page summariser (check wording before it goes on a slide).
Gathered to back the house writing rules for both decks.

| File | What it covers |
|---|---|
| [round4-ai-writing-patterns.md](round4-ai-writing-patterns.md) | Catalog of AI writing tells by category and model era (Wikipedia, Graphite, Pangram); the 2026 em-dash flip; measured tells of Claude Opus 5/5.5, GPT-6 and Gemini 3.1; the studies (Kobak excess vocabulary, Liang, Juzek & Ward, Reinhart PNAS, Russell ACL 2025 expert detectors, detector bias against plain writing, "delve" rising then falling); remedies from Orwell, federal plain language, GOV.UK, Pinker; vendor prompting advice on style; jargon research (definitions don't fix it); a 15-step revision checklist and a prompting recipe |

## Round 5 — 2026-11-04 (the state of coding harnesses)

Gathered for the *State of the Harness* deck (`../state-of-harnesses/`). Same
tags as rounds 3 and 4. Ten profile files were written by parallel research
agents. Each was then checked against primary sources by a separate fact-checker,
whose "Verification pass" section at the end of the file overrides the body.
A completeness critic found gaps, and four more files filled them, also verified.
Start with the synthesis: it carries every file's tags, lists conflicts between
files, and ends with presentation candidates and an "avoid on slides" list.

| File | What it covers |
|---|---|
| [round5-synthesis.md](round5-synthesis.md) | **Start here.** Landscape tables, the common core, ten axes where harnesses differ (with builders' quotes), philosophies by family, dated 2026 timeline, what vendors say is next, does the harness change outcomes, deployment table, conflicts, slide candidates, claims to avoid |
| [round5-claude-code.md](round5-claude-code.md) | Claude Code: loop, tools being removed, CLAUDE.md and memory, auto mode and its published miss rate, hooks, mods, philosophy (Cherny, Wu, Mann), 6-month changelog |
| [round5-openai-codex.md](round5-openai-codex.md) | Codex: one Rust core behind every surface, code mode (JS `exec`), `apply_patch` grammar, sandboxing, merge into ChatGPT, end of the -Codex model line, prompt contents |
| [round5-copilot-architecture.md](round5-copilot-architecture.md) | Copilot as a harness family: the Microsoft Copilot harness, Local vs Copilot harness in VS Code, per-model prompts and edit tools in the open code, third-party agents, Rust port, Fusion |
| [round5-cursor-cognition.md](round5-cursor-cognition.md) | Cursor (now SpaceX) and Cognition (Devin, Devin Desktop ex-Windsurf): own models, dropping the embeddings index, coordinator/worker designs, VM isolation |
| [round5-google-amazon-jetbrains.md](round5-google-amazon-jetbrains.md) | Antigravity and Gemini CLI, Jules shutdown, Kiro (specs, Cedar, Lean proofs), Q Developer folded into Kiro, JetBrains Junie and Air, ACP |
| [round5-oss-terminal.md](round5-oss-terminal.md) | OpenCode, Pi, Goose, Aider, Crush, Qwen Code, Kimi Code: loops, prompts, edit tools, stars, safety defaults |
| [round5-oss-ide-extensions.md](round5-oss-ide-extensions.md) | Cline, Roo Code (shut), Kilo Code, Continue (to Cursor), Zed and ACP |
| [round5-platforms-research.md](round5-platforms-research.md) | OpenHands, SWE-agent and mini-swe-agent, Amp, Factory, Augment, Warp, DeepSeek Harness |
| [round5-convergence-standards.md](round5-convergence-standards.md) | Standards (AGENTS.md, MCP, Skills, ACP, AAIF), edit formats, grep vs index, system prompt sizes, the shared loop, academic taxonomies |
| [round5-philosophy-direction.md](round5-philosophy-direction.md) | Defining essays and talks, axes of disagreement, 2026 shifts, survey data |
| [round5-harness-effect-evidence.md](round5-harness-effect-evidence.md) | Same model, different harness: papers, leaderboards, vendor studies; the 45.9% vs 55.4% misquote; what a presenter can honestly claim |
| [round5-adoption-market.md](round5-adoption-market.md) | Gartner MQ, Amplifying public-output index, Microsoft earnings, Octoverse, Stack Overflow, JetBrains, DORA, Thoughtworks Radar |
| [round5-enterprise-harnesses.md](round5-enterprise-harnesses.md) | Tabnine, GitLab Duo, Rovo Dev, IBM Bob, Qoder, Replit, TRAE, Mistral Vibe, Grok Build; deployment and data comparison for a bank |
| [round5-philosophy-addendum.md](round5-philosophy-addendum.md) | Primary-sourced philosophy quotes by family, filling gaps in the profiles |

## Where round 2 changes or contradicts round 1

1. **OpenAI's frontier is now GPT-6** (Astra, Sol/6.1 Sol, Luna). The URL behind
   `track2-openai-gpt5-prompting-guides.md` now serves the GPT-6 guide. GPT-5.x
   guidance is the previous generation.
2. **OpenAI's multi-agent guidance moved a little.** `track2-vendor-disagreements.md`
   §3 quotes the 2025 practical guide ("maximize a single agent's
   capabilities first"). The GPT-6 guide offers a prompt for harnesses that
   already run multiple agents, telling the model to delegate when it "could
   save time or improve quality". That is advice on how to use subagents, not
   on whether to start with them, so the 2025 position is not replaced.
3. **Copilot model list** (`track1-models.md`): Gemini 3.1 Pro, Opus 4.5, Opus
   4.6, Sonnet 4.5 and Raptor mini are gone (retired Sep 1). Added: Fable 5.1,
   Opus 5.5, Sonnet 5.5, GPT-6 models, Gemini 3.7/3.8 Flash, Grok 4.6/4.7,
   MAI-Code-1.1-Flash. `track1-custom-agents.md` has an example that names
   `Claude Opus 4.5`, which no longer exists in Copilot.
4. **Content exclusions** (`track1-context.md`): now honoured by the Copilot
   app and CLI; still not by VS Code Edit/Agent modes.
5. **Sandboxing** (`track1-other-surfaces.md` §7): local sandboxing is now a
   concrete, configurable preview feature in the Copilot app.
6. **Cloud agent firewall** (`track1-coding-agent.md`): it does not cover MCP
   server or setup-step processes. Round 1 did not record this limit.
7. **mini-swe-agent** (`track3-benchmarks.md`): "bash as its only tool" still
   holds, but v2 uses native tool calling by default. Do not say it avoids the
   tool-calling interface.
8. **SWE-bench Verified top score:** one round-2 source says ~88.6%; round 1's
   vendor-reported 95-96% stands. The 88.6% looks like an older snapshot.
9. **Opus 4.5 across three product harnesses** (`track3-benchmarks.md`
   scaffold table, `track3-benchmark-critiques.md`): round 1's "50.2%-55.4%,
   5.2 pp spread" is wrong. Augment's primary post gives Auggie 51.80%,
   Cursor 50.21%, Claude Code 49.75% (about a 2-point spread). The 55.4% is
   Opus 4.6 in a different post. The deck does not use this figure.
10. **llm-stats verification count** (`track3-benchmarks.md`): round 1's "1 of
   100 independently verified" (Jun 16) is now 0 of 116 on the live board.
11. **Scale SEAL scaffold:** the top entries on the SWE-bench Pro board are now
   run with mini-swe-agent, not SWE-Agent, and not every entry runs under the
   same settings.
12. **Prompt files are deprecated in VS Code** (`track1-prompt-files.md`):
   not loaded by Agent Host sessions; prompt-to-skill migration is on by
   default. Unannounced; GitHub docs still say public preview.
13. **Code review instruction files** (`track1-agents-md.md`,
   `track1-code-review.md`): code review now also reads `CLAUDE.md`,
   `GEMINI.md` and a new `REVIEW.md`, not AGENTS.md only.
14. **VS Code instruction precedence** (`track1-repo-custom-instructions.md`):
   VS Code docs dropped the personal > repo > org list and now say not to
   rely on any precedence. User instruction files no longer sync.
15. **VS Code location settings** (`track1-path-specific-instructions.md`,
   `track1-custom-agents.md`): `chat.instructionsFilesLocations` and
   `chat.agentFilesLocations` are deprecated; `/create-agent` works only in
   the Local agent.
16. **Hooks** (`track1-hooks.md`): VS Code hooks are no longer one feature;
   the Local harness fires 8 events, Copilot SDK hooks are GA. The CLI also
   reads `.claude/settings.json`. Hook timeouts fail open.
17. **Copilot Memory** (`track1-memory-spaces.md`): also used by agentic
   autofix; the 28-day timer can reset on use.
18. **Terminal-Bench** (`track3-benchmarks.md`): the board is now version
   4.0; round 1's 2.1 figures are two versions old.
19. **More retirements:** Opus 4.7, Gemini 3.5/3.6 Flash and Kimi K2.7 Code
   on Oct 2; GPT-5.5, GPT-5.4, GPT-5.4 mini, GPT-5 mini, Gemini 3.7 Flash and
   Grok 4.5 on Oct 19. Six of them are on the EU data-residency list.
20. **A round-2 refutation was wrong:** "Copilot harness GA in JetBrains" is
   true (changelog Aug 24). See `round2-copilot-changes.md` §7.

## Follow-up pass (2026-09-30): former gaps now covered

The gaps listed at the end of the first round-2 run were researched against
primary sources the same day:

- Copilot instructions, AGENTS.md, prompt files, custom agents, skills,
  hooks, Memory, Spaces, CLI, SDK, plugins and Agentic Workflows:
  `round2-copilot-changes.md` §9 and §10.
- Permission models and secrets handling: new file
  `round2-agent-permission-models.md`.
- Gemini 3.x guidance: `round2-frontier-model-guidance.md` §4.
- Independent results for the newest models: `round2-evals-and-benchmarks.md`
  §6.
- OpenAI's GPT-5.4 and GPT-5.3-Codex figures and the Meng et al. paper: read
  in full through a reader proxy and the Crossref API.

## Still open

- Network egress control for MCP servers on the Copilot cloud agent: no
  primary source describes one.
- Independent results for GPT-6 Sol, Luna and 6.1 Sol, and Sonnet 5.5: none
  exist yet on any board checked. No METR time horizon for any model newer
  than Mythos Preview.
- Classifier-based approvers (Claude `auto`, Codex `auto_review`): no vendor
  publishes miss rates.
- Several docs disagree with changelogs (JetBrains support matrices, code
  review instruction files, plugin hooks on the cloud agent). Recorded in
  `round2-copilot-changes.md` §9 and §10; test before relying on them.
