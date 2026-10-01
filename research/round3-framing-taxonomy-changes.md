---
url: https://claude.com/blog/a-field-guide-to-claude-fable-finding-your-unknowns, https://en.wikipedia.org/wiki/There_are_unknown_unknowns, https://inthesetimes.com/article/what-rumsfeld-doesn-know-that-he-knows-about-abu-ghraib, https://en.wikipedia.org/wiki/Johari_window, https://doi.org/10.1109/MTD.2014.9, https://pdfs.semanticscholar.org/3ab6/bd6fd72110a18f2d9d442cab03369a6017c5.pdf, https://doi.org/10.1016/j.infsof.2015.10.008, https://journals-sol.sbc.org.br/index.php/jserd/article/download/2671/2256/15441, https://doi.org/10.1016/j.infsof.2018.05.010, https://martinfowler.com/bliki/TechnicalDebtQuadrant.html, https://quality.arc42.org/articles/iso-25010-update-2023, https://github.blog/changelog/month/08-2026/, https://github.blog/changelog/month/09-2026/, https://github.blog/changelog/2026-08-24-copilot-harness-generally-available-in-copilot-for-jetbrains, https://github.blog/changelog/2026-08-31-selected-github-copilot-models-deprecated, https://github.blog/changelog/2026-09-01-claude-fable-5-1-generally-available-in-github-copilot, https://github.blog/changelog/2026-09-02-content-exclusions-generally-available-in-copilot-app-and-cli, https://github.blog/changelog/2026-09-03-upcoming-deprecation-of-selected-github-copilot-models, https://github.blog/changelog/2026-09-04-gpt-6-astra-is-generally-available-in-github-copilot, https://github.blog/changelog/2026-09-09-enterprise-managed-permissions-for-github-copilot-agent-operations, https://github.blog/changelog/2026-09-14-configure-cost-and-quality-in-copilot-auto-model-selection, https://github.blog/changelog/2026-09-18-upcoming-deprecation-of-selected-github-copilot-models-in-mid-october, https://github.blog/changelog/2026-09-22-claude-opus-5-5-is-now-available-in-github-copilot, https://github.blog/changelog/2026-09-22-openais-gpt-6-sol-and-gpt-6-luna-now-available, https://github.blog/changelog/2026-09-23-local-sandboxing-in-the-github-copilot-app, https://github.blog/changelog/2026-09-28-claude-sonnet-5-5-in-github-copilot, https://github.blog/changelog/2026-09-30-hydrafusion-in-vs-code-and-the-github-copilot-app, https://code.visualstudio.com/updates/v1_129, https://code.visualstudio.com/updates/v1_131, https://code.visualstudio.com/updates/v1_135, https://code.visualstudio.com/updates/v1_140, https://code.visualstudio.com/docs/agents/run/agent-harnesses, https://code.visualstudio.com/docs/agent-customization/prompt-files
fetched: 2026-10-01
---

# Round 3: knowns/unknowns framing, code issue taxonomy, Copilot changes Aug 13 to Oct 1

Round 3 file. Tags: [P] confirmed against the primary source on 2026-10-01, [S] secondary source, [R] refuted, [O] our recommendation (not sourced).

## 1. Does Anthropic use the "knowns and unknowns" framing?

**Verdict: yes, almost exactly.** It comes from one Anthropic staff member's post on the Claude blog, about Claude Fable 5 and Claude Code. It is not in Anthropic's docs or engineering blog as far as searches show.

- [P] "A field guide to Claude Fable 5: Finding your unknowns", Thariq Shihipar, "member of technical staff, Anthropic", claude.com blog, **July 6, 2026**.
  https://claude.com/blog/a-field-guide-to-claude-fable-finding-your-unknowns
- [P] Opening: "When working with Claude Code, I'm often reminded of the difference between the map and the territory. The map, a representation of the work to be done, is my prompts and skills and context, it's what I give Claude. The territory is where the work needs to happen, the codebase, the real world, its actual constraints."
- [P] "The difference between the map and the territory is what I call _unknowns_."
- [P] The four categories, verbatim:
  - "**Known Knowns:** This is essentially what is in my prompt. What do I tell the agent that I want?"
  - "**Known Unknowns:** What haven't I figured out yet, but I'm aware that I haven't?"
  - "**Unknown Knowns:** What's so obvious I'd never write it down, but would recognize it if I saw it?"
  - "**Unknown Unknowns:** What haven't I considered at all?"
- [P] Why it matters: "When Claude runs into an unknown, it needs to make a decision based on its best guess of what I want. The more work being done, the more unknowns Claude might run into."
- [P] Technique ("blind spot pass"): "I'm working on adding a new auth provider but I know nothing about the auth modules in this codebase. Can you do a blind spot pass to help me figure out my relevant unknown unknowns and help me prompt you better."
- [P] Closing: "Every explainer, brainstorm, interview, prototype, and reference is a cheap way to find out what you didn't know before it gets expensive to fix."
- [P] Section order: Knowing your unknowns; Help Claude help you; Pre-implementation; During implementation; Post implementation; How this comes together: launching Fable; Matching the Map and Territory.
- [P] The post does not mention Rumsfeld or the Johari window.

**Wording for a slide.** "Anthropic describes working with AI as mapping your knowns and unknowns" slightly overstates it. Safer: "An Anthropic field guide to Claude Code (Thariq Shihipar, claude.com, July 2026) sorts what you bring to a task into known knowns, known unknowns, unknown knowns and unknown unknowns, and calls the gap between your prompt and the real codebase 'unknowns'." Its metaphor is "the map and the territory", not "mapping". [O]

**Origins of the four-quadrant framing** (brief):

- [S] Donald Rumsfeld, US Department of Defense news briefing, **Feb 12, 2002**: "there are known knowns; there are things we know we know. We also know there are known unknowns; that is to say we know there are some things we do not know. But there are also unknown unknowns ... the ones we don't know we don't know." (Quoted from the DoD transcript via Wikipedia, "There are unknown unknowns"; the defense.gov transcript returned 403 to our fetch.)
- [S] Johari window: Joseph Luft and Harrington Ingham, "The Johari window, a graphic model of interpersonal awareness", Proceedings of the Western Training Laboratory in Group Development, UCLA, **1955**. Its four panes (open, blind, hidden, unknown) cross "known to self" with "known to others". It is a cousin of the Rumsfeld grid, not the same grid. (Wikipedia, "Johari window".)
- [P] "Unknown knowns": Slavoj Žižek, "What Rumsfeld Doesn't Know That He Knows About Abu Ghraib", In These Times, **May 21, 2004**: "the things we don't know that we know ... which is precisely, the Freudian unconscious". Note that Shihipar's "unknown knowns" (too obvious to write down) is closer to tacit knowledge than to Žižek's disavowed beliefs.

## 2. Code issue taxonomy for auditor agents

### 2.1 What the sources say

**Alves et al. 2014** [P] "Towards an Ontology of Terms on Technical Debt", Alves, Ribeiro, Caires, Mendes, Spínola, 6th Int. Workshop on Managing Technical Debt (MTD 2014), pp. 1-7, DOI 10.1109/MTD.2014.9. Checked against the authors' presentation PDF (Semantic Scholar mirror), not the IEEE paper text.
- Classifies debt by its "nature": "the activity of the development process execution where the debt was inserted".
- 13 types: Architecture, Build, Code, Defect, Design, Documentation, Infrastructure, People, Process, Requirement, Service, Test Automation, Test.
- Definitions, verbatim where readable:
  - Architecture: "problems encountered in project architecture, for example, violation of modularity, which can affect architectural requirements (performance, robustness, among others)."
  - Build: "build related issues that make this task harder, and more time/processing consuming unnecessarily ... if the build process needs to run ill-defined dependencies, the process becomes unnecessarily slow."
  - Code: "problems found in the source code which can affect negatively the legibility of the code making it more difficult to be maintained ... bad coding practices."
  - Defect: "known defects, usually identified by testing activities or by the user and reported on bug track systems" (partly garbled in the PDF; check the IEEE text before quoting).
  - Design: "practices which violated the principles of good object-oriented design (e.g. very large or tightly coupled classes)."
  - Documentation: "missing, inadequate, or incomplete documentation of any type."
  - Infrastructure: example "delaying an upgrade or infrastructure fix".
  - People: "expertise concentrated in too few people, as an effect of delayed training and/or hiring."
  - Process: "inefficient processes, e.g. what the process was designed to handle may be no longer appropriate."
  - Requirement: "requirements that are only partially implemented ... implemented but in a way that doesn't fully satisfy all the non-functional requirements (e.g. security, performance, etc.)."
  - Test Automation: "the work involved in automating tests of previously developed functionality to support continuous integration and faster development cycles."
- Documentation debt indicators listed: "Documentation does not exist", "Incomplete Documentation", "Insufficient comments in code", "Outdated Documentation", "Test Documentation".

**Alves et al. 2016** "Identification and management of technical debt: A systematic mapping study", Alves, Mendes, de Mendonça, Spínola, Shull, Seaman, Information and Software Technology 70:100-121, Feb 2016, DOI 10.1016/j.infsof.2015.10.008 [P metadata via Crossref; publisher page blocked].
- [S] 100 primary studies, 2010-2014. 15 types: "design, architecture, documentation, test, code, defect, requirements, infrastructure, people, test automation, process, build, service, usability, and versioning debts." Source: Murillo, López, Spínola, Guzmán, Rios, Pacheco, "Identification and Management of Technical Debt: A Systematic Mapping Study Update", JSERD 11:8, 2023, DOI 10.5753/jserd.2023.2671, co-authored by two of the original authors. So the 2016 list adds **usability** and **versioning** to the 2014 list.
- [S] Same 2023 update: "Some types of technical debt are presented in the three studies [Alves 2016, Li 2015, Rios 2018]: code, design, architecture, and test debt ... these particular types may be considered accepted technical debt types."
- [S] Same update: **security debt** ("vulnerabilities or exploitable weaknesses", Izurieta et al. 2018) and elasticity debt are new terms not in Alves 2016; "comments on source code were the most common indicator from 2015 to 2022" (self-admitted technical debt, SATD). Li et al. 2015 treat defects and process as not technical debt.

**Rios et al. 2018** [S] "A tertiary study on technical debt: Types, management strategies, research trends, and base information for practitioners", Rios, de Mendonça Neto, Spínola, Information and Software Technology 102:117-145, Oct 2018, DOI 10.1016/j.infsof.2018.05.010 (metadata [P] via Crossref). 13 secondary studies, 2012 to March 2018; a taxonomy of 15 TD types. Full list not confirmed against the paper.

**Fowler's Technical Debt Quadrant** [P] martinfowler.com/bliki/TechnicalDebtQuadrant.html, Oct 14, 2009. Two axes: "Not just is there a difference between prudent and reckless debt, there's also a difference between deliberate and inadvertent debt." The well-known quadrant captions ("We don't have time for design", "What's Layering?" etc.) are inside an image and could not be confirmed as page text. It classifies **intent**, not issue type, so a code auditor cannot apply it from code alone. [O]

**ISO/IEC 25010:2023** [S] (iso.org blocked; arc42 quality model summary). Nine product quality characteristics: functional suitability, performance efficiency, compatibility, interaction capability (renamed from usability), reliability, security, maintainability, flexibility (renamed from portability), safety (new in 2023).

### 2.2 Recommended auditor set [O]

Reasoning: start from the four types all three taxonomies agree on (code, design, architecture, test), add the types a code reader can see (documentation, build, infrastructure, versioning, defect), and add security, which Alves lacks but ISO 25010 and the 2023 update name. Drop people, process, service, usability and requirements debt: they need interviews, runtime data or product owners, not a read of the repo. Merge design and architecture so two agents do not fight over the same god class.

**Rules for every auditor** [O]
- Read only. Must NOT edit, format, move or delete files, commit, push, open PRs or issues, or install anything.
- Write only to its own findings doc. Each finding: id, file:line, severity, evidence (short quote), why it matters, suggested next step, confidence.
- Stay in its lane. Note out-of-scope issues in one line under "Handoffs" without investigating them.
- No guessing at intent (Fowler's deliberate vs inadvertent) unless a comment or commit says so.

| Auditor | Source types | Look for | Must NOT |
|---|---|---|---|
| 1. Code quality | Code debt [P] | Duplicated blocks; long or deeply nested functions; dead code and unused symbols; TODO/FIXME/HACK comments (SATD) | Judge architecture; rewrite code in the report; flag style a formatter or linter already enforces |
| 2. Design and architecture | Design + Architecture debt [P] | God classes and tight coupling; cyclic dependencies between modules; layer violations (UI calling the DB); modules that break the documented architecture | Propose a full redesign; count line-level smells (auditor 1's job) |
| 3. Tests | Test + Test Automation debt [P] | Critical paths with no tests; skipped, disabled or always-passing tests (no assertions); manual-only steps that could run in CI; tests that hit real external services | Run the suite against shared or production environments; write new tests |
| 4. Documentation (inline and external) | Documentation debt [P] | README or setup steps that no longer match the code; public APIs without docs; comments that contradict the code they describe; missing runbooks or decision records | Rewrite docs; flag missing comments on self-explanatory code |
| 5. Build, dependencies and infrastructure | Build + Infrastructure + Versioning debt [S] | Unpinned or end-of-life dependencies; unused or duplicate dependencies; slow, non-reproducible or ill-defined build steps; CI/IaC config drift between environments | Upgrade packages; run installs or builds with network access; touch pipelines |
| 6. Security | Security debt [S], ISO 25010 security [S] | Hardcoded secrets or keys; injection-prone string building (SQL, shell, paths); missing authorisation checks; dependencies with known CVEs; unsafe deserialisation | Print secret values (redact); run exploits or scanners against live systems; contact external services |
| 7. Defects and error handling | Defect debt [P], ISO 25010 reliability [S] | Swallowed or overly broad exceptions; unchecked nulls and unhandled edge cases; resource leaks (files, connections); known-bug comments and issue references in code | Reproduce bugs by running the app against real data; fix anything |

Optional eighth for a bank [O]: **Observability and operations** (logging of sensitive data, missing audit logs, no health checks). It overlaps 6 and 7, so add it only if those docs get too long.

## 3. What changed for a VS Code Copilot user, Aug 13 to Oct 1, 2026

All dates are GitHub changelog or VS Code release-note dates, checked against the live pages on 2026-10-01 [P] unless marked.

| Date | Change | Source |
|---|---|---|
| Aug 24 | The Copilot harness (the same agent runtime as the Copilot CLI and app) became generally available in Copilot for JetBrains. | github.blog/changelog/2026-08-24-copilot-harness-generally-available-in-copilot-for-jetbrains |
| Sep 1 | Claude Fable 5.1 became generally available in Copilot for Pro+, Max, Business and Enterprise. (Round 2 dated it Sep 4 from the weekly roundup; the dedicated entry is Sep 1.) | github.blog/changelog/2026-09-01-claude-fable-5-1-generally-available-in-github-copilot |
| Sep 1 | Six models were retired: Gemini 3.1 Pro, Claude Opus 4.5 and 4.6, Claude Sonnet 4.5 and 4.6, and Raptor mini. Sonnet 4.6 stays only for individuals on annual plans. | github.blog/changelog/2026-08-31-selected-github-copilot-models-deprecated |
| Sep 2 | The Copilot app and CLI now honour content exclusions. VS Code agent mode still does not. | github.blog/changelog/2026-09-02-content-exclusions-generally-available-in-copilot-app-and-cli |
| Sep 3-4 | Gemini 3.8 Flash arrived (Sep 3) and GPT-6 Astra became generally available (Sep 4, Pro+, Max, Business, Enterprise). | github.blog/changelog/2026-09-04-gpt-6-astra-is-generally-available-in-github-copilot |
| Sep 9 | Enterprise admins can now block, require approval for, or allow agent shell commands, file edits and network domains, and users cannot loosen these rules. Covers VS Code Agent Host sessions, the CLI and the app. | github.blog/changelog/2026-09-09-enterprise-managed-permissions-for-github-copilot-agent-operations |
| Sep 14 | Auto model selection gained three settings, Efficiency, Balance and Intelligence, in VS Code, the CLI and the app. | github.blog/changelog/2026-09-14-configure-cost-and-quality-in-copilot-auto-model-selection |
| Sep 3 and Sep 18 | More retirements were announced: Opus 4.7, Gemini 3.5/3.6 Flash and Kimi K2.7 Code on Oct 2; GPT-5.5, GPT-5.4, GPT-5.4 mini, GPT-5 mini, Gemini 3.7 Flash and Grok 4.5 on Oct 19. | github.blog/changelog/2026-09-03-upcoming-deprecation-of-selected-github-copilot-models; .../2026-09-18-upcoming-deprecation-of-selected-github-copilot-models-in-mid-october |
| Sep 22 | Claude Opus 5.5 (Pro+, Max, Business, Enterprise) and GPT-6 Sol and GPT-6 Luna arrived. | github.blog/changelog/2026-09-22-claude-opus-5-5-is-now-available-in-github-copilot; .../2026-09-22-openais-gpt-6-sol-and-gpt-6-luna-now-available |
| Sep 23 | The Copilot app gained local sandboxing (public preview, off by default) that limits the agent's file, network and credential access. It is not in VS Code. | github.blog/changelog/2026-09-23-local-sandboxing-in-the-github-copilot-app |
| Sep 28-29 | Claude Sonnet 5.5 became generally available on all paid plans including Pro (Sep 28), and GPT-6.1 Sol arrived (Sep 29). | github.blog/changelog/2026-09-28-claude-sonnet-5-5-in-github-copilot |
| Sep 30 | VS Code 1.140 headlines the Copilot harness: "In this release, it might already be the default selection for you." HydraFusion, which picks models per task, is a research preview the same day. | code.visualstudio.com/updates/v1_140; github.blog/changelog/2026-09-30-hydrafusion-in-vs-code-and-the-github-copilot-app |
| by Sep 30 (docs only, undated) | Prompt files (`.prompt.md`) are deprecated: Agent Host sessions do not load them, and migration to skills is on by default. Not announced in any changelog. | code.visualstudio.com/docs/agent-customization/prompt-files |

**Excluded because it predates Aug 13** [P]:
- The Agent Host and the harness picker: VS Code 1.129 (**Jul 15, 2026**) introduced "the agent host - a dedicated process that runs agent harnesses such as Copilot, Claude, and Codex", opt-in through `chat.agentHost.enabled`. VS Code 1.131 (**Jul 29**) says to "select an agent host harness from the harness dropdown". The docs now call this control **Session Target** (page dated 9/30/2026); when that name first appeared is not dated. On a slide, the change after Aug 13 is that the Copilot harness may now be the default (1.140), not that session targets exist.
- Agent Plugins 1.0 (Aug 12) and MAI-Code-1.1-Flash (Aug 11). Gemini 3.7 Flash landed on Aug 13 itself; Grok 4.6 (Aug 14) and Grok 4.7 (Sep 21) are minor additions.

**Smaller items a VS Code user may notice** [P from round 2, `round2-copilot-changes.md` §9]: VS Code docs dropped the instruction precedence order (Sep 23, 1.139 docs); `chat.instructionsFilesLocations` and `chat.agentFilesLocations` are deprecated (1.137 docs); VS Code 1.135 (Aug 26) put Local-agent sandboxing back to opt-in.
