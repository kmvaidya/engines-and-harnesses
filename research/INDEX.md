# Research index

38 files, all fetched **2026-08-12**. Every file opens with frontmatter carrying its
source URL(s) and fetch date. The deck (`../index.html`) is built from these files,
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
