---
url: https://www.anthropic.com/engineering/building-effective-agents, https://www.anthropic.com/engineering/multi-agent-research-system, https://cognition.com/blog/dont-build-multi-agents, https://cognition.com/blog/multi-agents-working, https://cognition.com/blog, https://ampcode.com/how-to-build-an-agent, https://ampcode.com/news, https://ampcode.com/news/the-coding-agent-is-dead, https://ampcode.com/news/gpt-5.3-codex, https://ampcode.com/news/who-cares-about-the-model, https://ampcode.com/news/less-noise, https://ampcode.com/news/amp-labs-westpac, https://cline.bot/blog/why-cline-doesnt-index-your-codebase-and-why-thats-a-good-thing, https://aider.chat/2023/12/21/unified-diffs.html, https://aider.chat/2023/10/22/repomap.html, https://cursor.com/blog, https://cursor.com/blog/semsearch, https://cursor.com/blog/self-driving-codebases, https://cursor.com/blog/third-era, https://cursor.com/blog/cursor-3, https://cursor.com/blog/joining-spacex, https://cursor.com/blog/agent-sdk, https://forum.cursor.com/t/what-do-you-think-about-cursor-removing-the-codebase-indexing-settings/165899, https://openai.com/index/harness-engineering/, https://openai.com/index/introducing-codex/, https://openai.com/index/unrolling-the-codex-agent-loop/, https://mitchellh.com/writing/my-ai-adoption-journey, https://www.martinfowler.com/articles/exploring-gen-ai/harness-engineering-memo.html, https://martinfowler.com/articles/harness-engineering.html, https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html, https://blog.langchain.com/the-anatomy-of-an-agent-harness/, https://rosetta.to/u/ycombinator/andrej-karpathy-software-is-changing-again, https://www.latent.space/p/s3, https://simonwillison.net/tags/andrej-karpathy/, https://simonwillison.net/2026/Feb/26/andrej-karpathy/, https://simonwillison.net/2025/Oct/18/agi-is-still-a-decade-away/, https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/, https://simonwillison.net/2025/Sep/18/agents/, https://simonwillison.net/2025/Sep/30/designing-agentic-loops/, https://simonwillison.net/2025/Oct/5/parallel-coding-agents/, https://simonwillison.net/2026/Feb/23/agentic-engineering-patterns/, https://ghuntley.com/ralph/, https://raw.githubusercontent.com/anthropics/claude-plugins-official/main/plugins/ralph-loop/README.md, https://steve-yegge.medium.com/welcome-to-gas-town-4f25ee16dd04, https://github.com/humanlayer/12-factor-agents, https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md, https://rosetta.to/u/ycombinator/inside-claude-code-with-its-creator-boris-cherny, https://survey.stackoverflow.co/2026/, https://survey.stackoverflow.co/2026/ai, https://survey.stackoverflow.co/2026/ai/data, https://blog.jetbrains.com/research/2026/08/ai-coding-agent-adoption-2026/, https://blog.jetbrains.com/research/2026/08/how-much-code-do-developers-really-let-agents-write/, https://github.blog/news-insights/octoverse/octoverse-commits-pushes-reach-new-highs-in-2026-as-developers-build-with-agents/, https://metr.org/blog/2026-02-24-uplift-update/, https://metr.org/blog/2026-05-11-ai-usage-survey/, https://metr.org/blog/, https://www.anthropic.com/news/anthropic-raises-30-billion-series-g-funding-380-billion-post-money-valuation, https://thenewstack.io/vibe-coding-is-passe-karpathy-has-a-new-name-for-the-future-of-software/, https://www.techzine.eu/news/devops/142197/spacex-acquires-cursor-for-60-billion/, https://kiro.dev/blog/kiro-and-the-future-of-software-development/, https://blog.jetbrains.com/blog/2026/09/22/introducing-jetbrains-air/, https://antigravity.google/blog/introducing-google-antigravity, https://forum.cursor.com/t/165899.json, https://latent.space/wiki/walden-yan-7c572c23/
fetched: 2026-11-04
verified: 2026-11-04 (adversarial pass; see last section)
---

# Coding harnesses: cross-cutting philosophy and direction (round 5, 2026-11-04)

**Tags.** [P] confirmed on the primary source: we fetched the author's or vendor's own page and checked the wording against the raw page text. [P\*] primary source, but the quote came back through a page summariser; check the wording before it goes on a slide. [S] secondary source only (news, third-party blogs, aggregators). [E] extracted from a source but not cross-checked; in this file it mostly means a speech quote taken from a third-party transcript of a talk or podcast (auto-captions, so filler words and mis-hearings are possible). [R] refuted or misquoted wording found circulating; recorded so nobody reuses it. [O] our own analysis, labelled. "(older than 6 months)" marks anything published before about May 2026. Where a claim is already documented in a sibling round-5 file, we cite that file and keep its tag rather than re-research it.

This file is the cross-cutting layer. Per-harness detail lives in `round5-claude-code.md`, `round5-copilot-architecture.md`, `round5-openai-codex.md`, `round5-cursor-cognition.md`, `round5-google-amazon-jetbrains.md` and `round5-oss-terminal.md`. Older doctrine (Anthropic and OpenAI agent guidance, the 80% thin-prompt post) is in the track2 files.

## Short version

- **The 2026 survey numbers moved a lot.** JetBrains (15,000+ professional developers, May to July 2026): 90% use coding agents at work at least weekly, 68% daily; Claude Code 39% at work (up from 18% in January), GitHub Copilot 21% (down from 29% a year earlier), Codex 16% (up from 3%), Cursor 12% (down from 18%) [P]. Stack Overflow 2026 (30,000+ respondents): among the 12,255 who answered the coding-agent question, Claude Code 65.5%, Copilot 58.7%, Codex 29.5%, Cursor 25.5% [P]. GitHub Octoverse (Oct 28, 2026): by September 2026, more than 40% of pull requests on GitHub started with an agent's first draft, up from 17% in March [P].
- **Productivity is still not measured cleanly.** METR's Feb 2026 rerun could not produce a trustworthy estimate because developers refused to work without AI; its May 2026 survey found a median self-reported 1.4 to 2x value change and 3x speed change, with METR warning these are "not necessarily grounded in reality" [P].
- **Multi-agent: the argument ended in a narrow truce.** Cognition argued in June 2025 that multi-agent systems are fragile; in April 2026 the same author wrote that what works is "multiple agents contribute intelligence to a task while writes stay single-threaded" [P]. Cursor's swarm research and Anthropic's research system reach a compatible position.
- **Grep beat the embeddings index, at least at Cursor.** Cursor published a +12.5% accuracy gain from semantic search in Nov 2025, then turned the embeddings index down in July 2026 because "models have gotten really good at using grep / indexed search" [P] (staff forum posts, not a blog announcement). Claude Code, Codex, Cline, Gemini CLI and Kiro were already grep-first. Copilot and JetBrains keep a semantic or IDE index.
- **"Harness engineering" has a traceable origin.** Mitchell Hashimoto named it on Feb 5, 2026 ("I've grown to calling this 'harness engineering'"), OpenAI's Codex team used it as a title on Feb 11, LangChain's "Agent = Model + Harness" followed on Mar 10, and Birgitta Böckeler (Thoughtworks) wrote the main framework on Apr 2 [P for Hashimoto, LangChain, Böckeler; P\* for the OpenAI date, since openai.com returned 403 on 2026-11-04]. Anthropic and OpenAI were already calling the agent loop a "harness" in late 2025 and Jan 2026.
- **The autonomy debate flipped direction inside 16 months.** Karpathy in June 2025: "keep the AI on the leash" and build "Iron Man suits" [E]. Karpathy in Feb 2026: "coding agents basically didn't work before December and basically work since" [P\*, wording confirmed on Simon Willison's page; tweet not fetched]. Amp in Sep 2026: "If you have the patience to watch your agents work, you're giving them too short a leash." [P] (corrected 2026-11-04: an earlier draft inserted "step-by-step" into this sentence; the page does not have it there)
- **Model choice is treated as a commodity by some harness makers and as the moat by others.** Amp swapped its default from Claude (Opus 4.8) to GPT (GPT-5.6 Sol) when it shipped the Dial, and got "Not a single complaint" [P]. Claude Code's lead says "never bet against the model" and that scaffolding gains of "10 20%" get "wiped out with the next model" [E]. Cursor, Cognition and Copilot all now train or tune their own models.
- **The market consolidated.** Cursor was acquired by SpaceX (closed Aug 14, 2026) and now ships Grok models [P]; Cognition (which bought Windsurf in 2025) passed $1B run-rate; Gemini CLI folded into Antigravity CLI; Jules, Amazon Q Developer and Kimi CLI were wound down (see sibling files).
- **Direction, stated and shipped:** agents that run without a human watching (cloud runners, schedules, `/goal` modes that loop until done), a manager view for many agents (Cursor 3 Agents Window, Devin Desktop, JetBrains Air, Copilot app, Amp's Puck), open protocols between agent and UI (ACP, AHP, AGENTS.md, Agent Skills), and review as the stated bottleneck.

---

## 1. The essays and talks that define stances

### 1.1 Simplicity: "an LLM, a loop, and enough tokens"

| Who, date | Verbatim | Tag, URL |
|---|---|---|
| Erik S. and Barry Zhang, Anthropic, Dec 19, 2024 (older than 6 months) | "we recommend finding the simplest solution possible, and only increasing complexity when needed." Agents "are typically just LLMs using tools based on environmental feedback in a loop." | [P] anthropic.com/engineering/building-effective-agents |
| Thorsten Ball, Amp, Apr 15, 2025 (older than 6 months) | "It's an LLM, a loop, and enough tokens." Builds a working agent in "less than 400 lines of code, most of which is boilerplate." | [P] ampcode.com/how-to-build-an-agent |
| Simon Willison, Sep 18, 2025 (older than 6 months) | "An LLM agent runs tools in a loop to achieve a goal." | [P] simonwillison.net/2025/Sep/18/agents/ |
| Boris Cherny (Claude Code), YC Light Cone, published Feb 17, 2026 (older than 6 months) | "we have a framed copy of the bitter lesson on the wall ... what it boils down to is never bet against the model." On harness code ("scaffolding"): "depending on the domain you can improve performance maybe 10 20% something like that and then essentially the gain is wiped out with the next model." | [E] transcript at rosetta.to/u/ycombinator/inside-claude-code-with-its-creator-boris-cherny |
| Amp team, Feb 19, 2026 (older than 6 months) | "With the newest models, the agent — the prompts and tools you wrap around a model — is no longer the limiting factor." "A simple tool called `bash` is often enough." "How you organize your codebase for agents, how your organization uses them — those are now the bottlenecks." | [P] ampcode.com/news/the-coding-agent-is-dead |

- [P] Cherny's other statements ("thinnest possible wrapper", "We unship tools all the time", ablation of the system prompt per model, "every six months, delete your [CLAUDE.md]") are in `round5-claude-code.md` §8. Mario Zechner's "if I don't need it, it won't be built" and Pi's 2026 reversal on MCP are in `round5-oss-terminal.md` §6.
- [E] The YC transcript renders the bitter-lesson line as "the more general model will always be the more specific model", a captioning error for "beat". Quote only "never bet against the model".
- [O] The simplicity camp agrees on the loop and disagrees on what to do with the spare engineering time. Anthropic and Amp spend it on deleting harness code as models improve; Cursor, Cognition and GitHub spend it on infrastructure around the loop (cloud runners, routers, own models).

### 1.2 Code search and edit formats: early stances that still shape tools

- [P] Paul Gauthier, Aider, Oct 22, 2023 (older than 6 months): "aider sends GPT a concise map of your whole git repository that includes the most important classes and functions", ranked with "a graph ranking algorithm". https://aider.chat/2023/10/22/repomap.html
- [P] Gauthier, Dec 21, 2023 (older than 6 months): "Unified diffs make GPT-4 Turbo 3X less lazy"; score went from "20% as a baseline" to "61%". Edit-format principles: "FAMILIAR", "SIMPLE - Choose a simple format that avoids escaping, syntactic overhead and brittle specifiers", "HIGH LEVEL", "FLEXIBLE". https://aider.chat/2023/12/21/unified-diffs.html. [O] This was the first public evidence that harness choices (edit format) move scores by tens of points with the model fixed.
- [P] Nick Baumann, Cline, May 27, 2025 (older than 6 months): "when you chunk code for embeddings, you're literally tearing apart its logic." "An index, by definition, is a snapshot frozen in time." "Your codebase isn't just text – it's your competitive advantage." https://cline.bot/blog/why-cline-doesnt-index-your-codebase-and-why-thats-a-good-thing
- [P] Cherny, May 2025: Claude Code first used RAG, then "landed on just agentic search"; the evidence was "mostly vibes" (verbatim in `round5-claude-code.md` §3).
- [P] Cursor, Nov 6, 2025 (older than 6 months), the counter-position: semantic search gave "12.5% higher accuracy in answering questions (6.5%–23.5% depending on the model)"; "the combination of these two leads to the best outcomes." https://cursor.com/blog/semsearch
- [P] Cursor staff, July 21-31, 2026, the reversal (thread opened by a user on Jul 16 after the indexing settings disappeared): "models have gotten really good at using grep / indexed search"; "the older dedicated semantic search path was rapidly no longer helping in a meaningful way" (Maxime, staff, Jul 21); "Semantic/embeddings indexing is being turned down in favor of grep-based retrieval" (Colin, Jul 22); the local grep index has "no embeddings involved anywhere in it" (Mohit, Jul 31). https://forum.cursor.com/t/what-do-you-think-about-cursor-removing-the-codebase-indexing-settings/165899
- [S] A Cursor docs page captured in June 2026 still described semantic search; the forum posts are later and come from staff.

### 1.3 Context engineering

- [P] Dex Horthy, HumanLayer, "12-Factor Agents" (repo first published around April 2025, older than 6 months): production agents are "mostly deterministic code, with LLM steps sprinkled in at just the right points". Factors include "Own your prompts", "Own your context window", "Own your control flow", "Small, Focused Agents", "Make your agent a stateless reducer". https://github.com/humanlayer/12-factor-agents
- [P] HumanLayer, "Advanced Context Engineering for Coding Agents" (undated; references Aug 2025, older than 6 months): "frequent intentional compaction", defined as "designing your ENTIRE WORKFLOW around context management"; research, plan, implement; "keeping utilization in the 40-60% range" (the doc writes it both as "40-60%" and "40%-60%"). The review argument: "A bad line of code is… a bad line of code. But a bad line of a plan could lead to hundreds of bad lines of code." "When you review the research and the plans, you get more leverage than you do when you review the code." https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md
- [P\*] Karpathy, Jun 27, 2025, as quoted by Simon Willison: "context engineering is the delicate art and science of filling the context window". https://simonwillison.net/tags/andrej-karpathy/ (older than 6 months)
- [P\*] OpenAI Codex team, Feb 11, 2026 (openai.com returned 403 to every fetcher on 2026-11-04, so this wording was not re-seen on the primary page; the ~100-line AGENTS.md detail is consistent across several secondary write-ups): "give Codex a map, not a 1,000-page instruction manual." "So instead of treating `AGENTS.md` as the encyclopedia, we treat it as the table of contents." "A short `AGENTS.md` (roughly 100 lines) is injected into context and serves primarily as a map". https://openai.com/index/harness-engineering/
- [O] Context engineering and spec-driven development (§1.6) share one claim: the leverage point for a human is the plan or the map, and line-by-line code review is the expensive fallback.

### 1.4 Single agent vs multi-agent

**June 2025: the two founding positions, one day apart.**

- [P] Walden Yan, Cognition, "Don't Build Multi-Agents", Jun 12, 2025 (older than 6 months): "it is evident that in 2025, running multiple agents in collaboration only results in fragile systems." "The simplest way to follow the principles is to just use a single-threaded linear agent". Principles [P]: "Share context, and share full agent traces, not just individual messages"; "Actions carry implicit decisions, and conflicting decisions carry bad results". https://cognition.com/blog/dont-build-multi-agents
- [P] Anthropic, "How we built our multi-agent research system", Jun 13, 2025 (older than 6 months): multi-agent "outperformed single-agent Claude Opus 4 by 90.2% on our internal research eval"; uses "about 15× more tokens than chats"; "token usage by itself explains 80% of the variance". And the caveat that both sides quote: "most coding tasks involve fewer truly parallelizable tasks than research" and domains "that require all agents to share the same context" are "not a good fit for multi-agent systems today." https://www.anthropic.com/engineering/multi-agent-research-system
- [O] These two posts agree more than the "Cognition vs Anthropic" framing suggests: both say coding is a poor fit for parallel writers.

**2026: the experiments and the truce.**

- [P] Steve Yegge, "Welcome to Gas Town", Jan 1, 2026 (older than 6 months): "Gas Town helps you with the tedium of running lots of Claude Code instances." His eight stages end at "Stage 6: CLI, multi-agent, YOLO. You regularly use 3 to 5 parallel instances", "Stage 7: 10+ agents, hand-managed", "Stage 8: Building your own orchestrator". His own warning: "You probably don't want to use it yet." and "It's also 100% vibe coded. I've never seen the code". Workers are "Polecats", the coordinator is "The Mayor", and all state lives in Git-backed "Beads". https://steve-yegge.medium.com/welcome-to-gas-town-4f25ee16dd04 (not re-verified on 2026-11-04: Medium returned 403; treat as [P\*] until re-read)
- [P] Wilson Lin, Cursor, "Towards self-driving codebases", Feb 5, 2026 (older than 6 months): "most runs would peak at several hundred agents" (corrected 2026-11-04; earlier draft had the non-verbatim "typically peaked at several hundred agents"), "~1,000 commits per hour across 10M tool calls over a period of one week" building a browser. Shared-state locking failed ("20 agents would slow to the throughput of 1-3"); a single executor "claim[ed] premature completion"; the design that worked was recursive planners plus workers, each worker on "their own copy of the repo", accepting an error rate that "remains small and constant, perhaps rarely completely clean but steady and manageable" (corrected 2026-11-04; the earlier quoted phrase "a small, steady error rate" is a paraphrase, not on the page). https://cursor.com/blog/self-driving-codebases
- [P] Walden Yan, "Multi-Agents: What's Actually Working", Apr 22, 2026: "A lot has changed since then." What works: "setups where multiple agents contribute intelligence to a task while writes stay single-threaded." "The practical shape is map-reduce-and-manage: a manager splits work, children execute, the manager synthesizes and reports back." Rejected: "the unstructured-swarm approach, arbitrary networks of agents negotiating with each other, is mostly a distraction." Open: "The open problems are all communication problems." https://cognition.com/blog/multi-agents-working
- Shipped counterparts: Claude Code agent teams ("Experimental and disabled by default", 2.1.32, Feb 5, 2026) [P, `round5-claude-code.md`]; Cursor Projects ("coordinator + thousands of subagents", Sep 10, 2026) [P, `round5-cursor-cognition.md`]; Amp "Agents can spawn other agents, message them, and exchange files across Amp threads" (Jul 17, 2026) [P, ampcode.com/news index]; Kiro's own trace analysis found and fixed "over-eager subagent delegation" (Oct 20, 2026) [P\*, `round5-google-amazon-jetbrains.md` §2.3].
- [O] Where it landed in late 2026: one writer, many readers. Read-only research subagents, clean-context reviewers and a manager that merges are common to Claude Code, Codex, Cursor, Devin, Copilot and Kiro. Parallel writers are used only with isolation (worktrees, separate VMs, separate repos) and a merge step. Cursor's swarm is the exception and runs on a throwaway research project.

### 1.5 Autonomy: leash, slider, loop

**Karpathy, in sequence.**

- [E] YC AI Startup School, "Software Is Changing (Again)", Jun 17, 2025 (older than 6 months), third-party transcript: "there's what I call the autonomy slider ... you are in charge of the autonomy slider and depending on the complexity of the task at hand you can uh tune the amount of autonomy". "we have to keep the AI on the leash ... it's not useful to me to get a diff of 10,000 lines of code to my repo. Like I have to I'm still the bottleneck". "it's less Iron Man robots and more Iron Man suits that you want to build. It's less like building flashy demos of autonomous agents and more building partial autonomy products." "when I see things like oh 2025 is the year of agents I get very concerned and I kind of feel like you know this is the decade of agents". https://rosetta.to/u/ycombinator/andrej-karpathy-software-is-changing-again (Latent Space's annotated transcript is paywalled: latent.space/p/s3)
- [P\*] (wording confirmed on Willison's raw page) Dwarkesh interview, Oct 2025, via Simon Willison Oct 18, 2025 (older than 6 months): "The reason you don't do it today is because they just don't work." Willison reports Karpathy found Claude Code and Codex CLI "didn't work well enough at all and net unhelpful" for nanochat (a paraphrase of a tweet). https://simonwillison.net/2025/Oct/18/agi-is-still-a-decade-away/
- [P\*] (wording confirmed on Willison's raw page, with a curly apostrophe in "didn’t") Feb 2026, via Simon Willison Feb 26, 2026 (older than 6 months): "coding agents basically didn't work before December and basically work since". Original: https://twitter.com/karpathy/status/2026731645169185220 (not fetched; X blocks readers). https://simonwillison.net/2026/Feb/26/andrej-karpathy/
- [S] "Agentic engineering": secondary coverage dates Karpathy's coinage to early February 2026 (the first anniversary of "vibe coding") and has him repeating it at Sequoia AI Ascent on Apr 30, 2026. One article quotes "You are orchestrating agents who do and acting as oversight." We could not reach the original post. https://thenewstack.io/vibe-coding-is-passe-karpathy-has-a-new-name-for-the-future-of-software/
- [P] Simon Willison adopted the term on Feb 23, 2026: agentic engineering is "professional software engineers using coding agents to improve and accelerate their work", against vibe coding as "coding where you pay no attention to the code at all". https://simonwillison.net/2026/Feb/23/agentic-engineering-patterns/

**The loop that does not stop.**

- [P] Geoffrey Huntley, "Ralph", Jul 14, 2025 (older than 6 months): "Ralph is a technique. In its purest form, Ralph is a Bash loop." `while :; do cat PROMPT.md | claude-code ; done`. "the technique is deterministically bad in an undeterministic world." "Building software with Ralph requires a great deal of faith and a belief in eventual consistency." https://ghuntley.com/ralph/
- [P] Productised by Anthropic: the official `ralph-loop` plugin (first commit Jan 6, 2026) implements Ralph "using a **Stop hook** that intercepts Claude's exit attempts" and credits Huntley ("Ralph is a Bash loop"). https://raw.githubusercontent.com/anthropics/claude-plugins-official/main/plugins/ralph-loop/README.md
- [O] The same idea is now a built-in mode in the main harnesses: Codex `/goal` (out of experimental May 2026, `round5-openai-codex.md`), Claude Code `/goal` (`round5-claude-code.md`), Cursor `/goal` (Aug 19, 2026, `round5-cursor-cognition.md`). Amp agents "can now set their own schedules, wake themselves up, and keep working" (Jul 21, 2026) [P, ampcode.com/news].

**Practitioners on how much to let go.**

- [P] Mitchell Hashimoto, "My AI Adoption Journey", Feb 5, 2026 (older than 6 months): "Step 6: Always Have an Agent Running". "I'd say right now I'm maybe effective at having a background agent running 10 to 20% of a normal working day." https://mitchellh.com/writing/my-ai-adoption-journey
- [P] Simon Willison, Oct 5, 2025 (older than 6 months): "I was pretty skeptical about this at first"; "the natural bottleneck on all of this is how fast I can review the results." https://simonwillison.net/2025/Oct/5/parallel-coding-agents/
- [P] Mario Zechner, Mar 25, 2026 (older than 6 months): "Set yourself limits on how much code you let the clanker generate per day, in line with your ability to actually review the code." (verbatim in `round5-oss-terminal.md` §6)
- [P] Amp, Sep 25, 2026: "If you have the patience to watch your agents work, you're giving them too short a leash." ([R] the version "watch your agents work step-by-step, you're giving them..." is a misquote from an earlier draft; "step-by-step" appears only in the post's first sentence, about collapsing "your agent's step-by-step work".) Amp now collapses tool steps because users care about "what the agent did, not how it got there" [P]. https://ampcode.com/news/less-noise
- [P] Stack Overflow 2026: "48% indicate they trust AI when they can easily validate the answers and only 16% extend that trust to most tasks that are not important work decisions." "That's why human-in-the-loop is the dominant mode of working with these tools." https://survey.stackoverflow.co/2026/ai

**Asynchronous delegation as a design goal.**

- [P\*] (openai.com 403 on 2026-11-04; not re-seen) OpenAI, Codex launch, May 16, 2025 (older than 6 months): "a cloud-based software engineering agent that can work on many tasks in parallel". "we believe the asynchronous, multi-agent workflow introduced by Codex in ChatGPT will become the de facto way engineers produce high-quality code." "Ultimately, we see these two modes of interaction—real-time pairing and task delegation—converging." https://openai.com/index/introducing-codex/
- [P] Michael Truell, Cursor, "The third era", Feb 26, 2026 (older than 6 months): era three "is defined by agents that can tackle larger tasks independently, over longer timescales, with less human direction." Internal data: "Thirty-five percent of the PRs we merge internally at Cursor are now created by agents operating autonomously in cloud VMs"; "2x as many agent users as Tab users". https://cursor.com/blog/third-era
- [P] Google, Antigravity launch, Nov 18, 2025 (older than 6 months), the counterweight: "A core failing of a remote-only form factor is the inability to iterate easily with the agent." (verbatim in `round5-google-amazon-jetbrains.md` §1.5)

### 1.6 Spec-first vs conversational

- [P] Marc Brooker, Kiro, Jul 15, 2025 (older than 6 months): "A specification is a kind of (version controlled, human-readable) super prompt." (more in `round5-google-amazon-jetbrains.md` §2.4). Kiro restated the stance on Jul 14, 2026: "developers deserve better than vibe coding."
- [P] Birgitta Böckeler, "Understanding Spec-Driven-Development: Kiro, spec-kit, and Tessl", Oct 15, 2025 (older than 6 months). Three levels: "Spec-first", "Spec-anchored", "Spec-as-source" ("only the spec is edited by the human, the human never touches the code"). Critiques: "To be honest, I'd rather review code than all these markdown files." For a small Kiro bug fix "the workflow was like using a sledgehammer to crack a nut." "I'm very skeptical that lots of up-front spec design is a good idea." "Are we making something worse in the attempt of making it better?" https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html
- [O] Spec-first survived as plan mode. Claude Code, Codex, Cursor, Gemini/Antigravity (`/plan`, Sep 22, 2026) and Copilot all have a plan step; Kiro is the only major harness whose default output is a set of spec files (`requirements.md`, `design.md`, `tasks.md`). Kiro itself added "Quick Spec" with "no approval gates" (`round5-google-amazon-jetbrains.md`), which reads as a response to the overhead critique.

### 1.7 Where "harness engineering" came from

| Date | Who | What they wrote | Tag |
|---|---|---|---|
| Nov 26, 2025 | Anthropic | "Effective harnesses for long-running agents": the noun "harness" for the code around the model | [P] `track2-anthropic-long-running-harnesses.md` |
| Jan 23, 2026 | OpenAI | "This post focuses on the Codex _harness_, which provides the core agent loop and execution logic that underlies all Codex experiences" | [P] openai.com/index/unrolling-the-codex-agent-loop/ |
| Feb 5, 2026 | Mitchell Hashimoto | "I don't know if there is a broad industry-accepted term for this yet, but I've grown to calling this "harness engineering."" "It is the idea that anytime you find an agent makes a mistake, you take the time to engineer a solution such that the agent never makes that mistake again." Two forms: "Better implicit prompting (AGENTS.md)" and "Actual, programmed tools." | [P] mitchellh.com/writing/my-ai-adoption-journey (dated February 5, 2026 on the page) |
| Feb 11, 2026 | Ryan Lopopolo, OpenAI | Title "Harness engineering: leveraging Codex in an agent-first world". "Humans steer. Agents execute." The team's job became to "design environments, specify intent, and build feedback loops that allow Codex agents to do reliable work." | [P\*] openai.com/index/harness-engineering/ (403 on 2026-11-04; title, author and Feb 11 date corroborated by Böckeler's memo and mirrors; quotes not re-seen) |
| Feb 17, 2026 | Birgitta Böckeler | Notes the OpenAI article "only mentions "harness" once in the text" and links the term to Hashimoto. Likes "harness" for "the tooling and practices we can use to keep AI agents in check." Critique: "What I am missing in the write-up is verification of functionality and behaviour." | [P] martinfowler.com/articles/exploring-gen-ai/harness-engineering-memo.html |
| Mar 10, 2026 | LangChain blog | "Agent = Model + Harness." "If you're not the model, you're the harness." "A harness is every piece of code, configuration, and execution logic that isn't the model itself." | [P] blog.langchain.com/the-anatomy-of-an-agent-harness/ |
| Apr 2, 2026 | Böckeler | "The term harness has emerged as a shorthand to mean everything in an AI agent except the model itself". "Guides (feedforward controls) - anticipate the agent's behaviour and aim to steer it _before_ it acts." "Sensors (feedback controls) - observe _after_ the agent acts and help it self-correct." "Not every codebase is equally amenable to harnessing." | [P] martinfowler.com/articles/harness-engineering.html |

- [P\*] OpenAI harness-engineering numbers (an earlier pass read these through a reader proxy; on 2026-11-04 openai.com returned 403 and the proxy route was not used, so they were not re-seen on the primary page. Corroboration: an exact-phrase web search matches "roughly 1,500 pull requests have been opened and merged with a small team of just three engineers driving Codex" on several mirrors, and Böckeler's memo independently says "over 1 million lines of code"): first commit "late August 2025"; "on the order of a million lines of code"; "roughly 1,500 pull requests have been opened and merged with a small team of just three engineers driving Codex", "3.5 PRs per engineer per day", and throughput "increased as the team has grown to now seven engineers"; "humans never directly contributed any code". On drift: "Our team used to spend every Friday (20% of the week) cleaning up "AI slop."" They replaced that with "golden principles" and recurring background Codex tasks: "This functions like garbage collection." Their own limit: "What we don't yet know is how architectural coherence evolves over years in a fully agent-generated system."
- [R] "OpenAI coined harness engineering": Hashimoto used the phrase six days earlier and said he did not know of an established term. Böckeler's memo makes the same link. Safer wording: "named by Mitchell Hashimoto, popularised by OpenAI and Thoughtworks in February 2026".
- [R] "Three engineers wrote 1M lines": the post says three engineers drove the first ~1,500 PRs and the team grew to seven. It is an internal product with "hundreds of users internally". Codex wrote the code; humans wrote none.
- Note for `round5-openai-codex.md`: that file tags the harness-engineering post [S] because openai.com returned 403. An earlier pass read the full text through a reader proxy; the verification pass on 2026-11-04 could not repeat that, so treat the claims as [P\*] (well corroborated, not re-seen on openai.com).
- [O] Böckeler's guides/sensors split maps directly onto a bank's controls vocabulary: instructions, skills and specs are preventive controls; tests, linters, type checks, review agents and hooks are detective controls.

### 1.8 Safety stance (pointer)

- [P] Simon Willison, Jun 16, 2025 (older than 6 months): the lethal trifecta is "Access to your private data", "Exposure to untrusted content", and "The ability to externally communicate in a way that could be used to steal your data". "The only way to stay safe there is to avoid that lethal trifecta combination entirely." https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/ (fuller treatment in `round2-agent-security-governance.md`).
- [P] Willison, Sep 30, 2025 (older than 6 months): "A critical new skill to develop is designing agentic loops." Options for YOLO mode: sandbox ("Run your agent in a secure sandbox that restricts the files and secrets it can access"), "Use someone else's computer.", or "Take a risk!" https://simonwillison.net/2025/Sep/30/designing-agentic-loops/
- [O] Willison's "someone else's computer" is now the default product shape (cloud agents, Amp orbs, Cursor and Copilot cloud VMs, Kiro Web). The vendors present it as convenience; it is also the cheapest sandbox.

---

## 2. Axes of disagreement, with harnesses placed on each

Placements are [O] judgements built from the cited evidence. Each row names the evidence and its tag.

### Axis A. Autonomy: human watches each step vs agent runs unwatched

| Position | Harness | Evidence |
|---|---|---|
| Watch and approve | Copilot Local harness default, Aider (git undo instead of prompts), Kiro spec gates | approval modes in `round2-agent-permission-models.md`; Kiro specs [P] |
| Slider, user picks | Claude Code (permission modes incl. classifier `auto`), Codex (`auto_review`), Antigravity, Cursor | `round5-claude-code.md`, `round5-openai-codex.md` [P] |
| Delegate and review the result | Codex Cloud, Copilot cloud agent, Devin, Cursor cloud agents, Kiro Web | Codex launch [P\*]; Cursor "third era" [P] |
| Unwatched by design | Amp ("too short a leash"), Gas Town (Stage 8), Ralph/`/goal` loops, Pi (YOLO default, no permission system) | Amp Sep 25, 2026 [P]; Yegge [P]; `round5-oss-terminal.md` [P] |

[O] Evidence that the centre of gravity moved: Copilot cloud agent usage "grew 230% year over year, against 85% for agent chat" (Octoverse [P]). The counter-evidence: SO 2026 says human-in-the-loop "is the dominant mode" [P], and METR could not keep developers in a no-AI arm, which says people want the tools, not that they trust them unwatched.

### Axis B. One agent vs many

| Position | Who | Evidence |
|---|---|---|
| Single thread | Cognition 2025, Pi (no built-in subagents), Aider | Yan Jun 2025 [P]; `round5-oss-terminal.md` [P] |
| One writer, many readers | Cognition 2026, Claude Code subagents, Codex, Copilot, Kiro, Devin | Yan Apr 2026 [P] |
| Managed swarm with isolation | Cursor Projects and research swarm, Gas Town, Claude Code agent teams (experimental), Amp agent-to-agent | Lin Feb 2026 [P]; Yegge [P\*, not re-verified]; Amp Jul 17 [P] |

### Axis C. How the agent finds code: grep vs index vs map

| Position | Who | Evidence |
|---|---|---|
| Grep/glob, no index | Claude Code, Codex (`rg`), Cline, Gemini CLI, Kiro, OpenCode 2 (dropped LSP), Pi | Cline May 2025 [P]; sibling files [P] |
| Grep with a local fast index, embeddings removed | Cursor (Instant Grep, since Jul 2026) | Cursor forum [P] |
| Grep plus semantic index | Copilot (`semantic_search`, semantic search on by default for online sessions) | `round5-copilot-architecture.md` [P] |
| IDE code model | Junie ("your IDE's semantic index") | `round5-google-amazon-jetbrains.md` [P\*] |
| Ranked repo map | Aider | Gauthier 2023 [P] |

[O] This axis has nearly collapsed. The one vendor that published a measured win for embeddings (Cursor) turned them off eight months later and gave model improvement as the reason. Copilot and JetBrains are the remaining index users, and both have an IDE that already holds an index.

### Axis D. Model coupling: one vendor vs any model

| Position | Who | Evidence |
|---|---|---|
| Lab harness, own models only | Claude Code (Claude), Codex (OpenAI models, per-model tuning in `models.json`), Antigravity (Gemini first, others via Vertex) | sibling files [P] |
| Multi-model, plus own models | Cursor (Composer, then Grok 4.6/4.7 after SpaceX), Cognition (SWE-2 on Kimi K3, SWE-2 Flash), Copilot (multi-vendor, own fine-tunes, Fusion routing) | `round5-cursor-cognition.md`, `round5-copilot-architecture.md` [P] |
| Model-agnostic by principle | JetBrains ("the future of agentic development will be multi-vendor"), OpenCode, Goose, Aider, Pi, Kiro, Amp | Skrygan Sep 22, 2026 [P]; Amp [P] |

- [P] Amp, Jul 29, 2026: "Most Amp users switched from Anthropic to OpenAI overnight." "Not a single complaint." "The differences between frontier models are now small." The next paragraph qualifies it: "But they still matter to us, here at Amp: across every thread on every tier, small differences compound, so we keep benchmarking and swapping models." [P] They name three things that matter more than the model: "how hard the task is, what context you put in, and how closely you review what comes out." The swap was Claude Opus 4.8 ("smart") to GPT-5.6 Sol ("medium") via the Dial; smart went from 55% of new threads to zero in a week. https://ampcode.com/news/who-cares-about-the-model
- [P] LangChain, Mar 10, 2026, on co-training: "Useful primitives are discovered, added to the harness, and then used when training the next generation of models. As this cycle repeats, models become more capable within the harness they were trained in." "But this doesn't mean that the best harness for your task is the one a model was post-trained with." They cite Terminal-Bench 2.0, where "Opus 4.6 in Claude Code scores far below Opus 4.6 in other harnesses" (possibly stale; TB is now on version 4.0, see `round2-evals-and-benchmarks.md`).
- [P] GitHub Octoverse: "In September 2026, 61% of GitHub Copilot users who selected a model themselves used more than one model", and "no single model carried more than 25% of requests that month."
- [P] Qwen Code: seven harness versions scored 76.40% to 77.80% on SWE-bench Verified with the model fixed (`round5-oss-terminal.md` §7). [O] Harness changes inside one product move scores little; switching harness families or edit formats can move them a lot (Aider 20% to 61%; OpenAI's ARC-AGI-3 13.3% to 38.3% in `round5-openai-codex.md`).

### Axis E. Surface: IDE vs terminal vs cloud vs agent manager

| Position | Who | Evidence |
|---|---|---|
| Left the editor | Amp killed its VS Code and Cursor extensions on Mar 5, 2026: "By keeping these new models in an editor sidebar, we restrict them." | [P] ampcode.com/news/the-coding-agent-is-dead |
| Rebuilt the IDE around agents | Cursor 3 "Agents Window" (Apr 2, 2026): "Engineers are still micromanaging individual agents"; "building this new interface from scratch, centered around agents". Antigravity: "surfaces are embedded into the agent". | [P] cursor.com/blog/cursor-3; [P] Google |
| IDE as the trust surface | JetBrains: "Code becomes cheaper to generate but more expensive to verify." Junie uses the IDE debugger and index. | [P] Skrygan |
| One harness, every surface | Copilot (CLI, app, SDK, VS Code, JetBrains on one harness), Kiro (`one-agent` post), Codex (CLI, IDE, cloud on one harness), Antigravity CLI and App | sibling files [P] |

[O] Nobody now argues for one surface. The argument is about which surface is primary. Amp and Cursor moved the primary surface to a list of running agents; Copilot and Kiro put one harness behind all surfaces; JetBrains argues the IDE is where verification happens.

### Axis F. Minimal vs batteries-included

| Minimal | Batteries-included |
|---|---|
| Pi (four tools, sub-1,000-token prompt), mini-swe-agent (bash only), Claude Code's stated "thinnest possible wrapper" and routine unshipping, Amp "A simple tool called `bash` is often enough" | Gas Town ("Gas Town is complicated"), Kiro (specs, hooks, steering, Crew), Copilot (14+ hook events, memory, spaces, plugins, Fusion), Devin |

[O] The minimal camp still added features: Pi added MCP in Sep 2026; Claude Code has 33 hook events, skills, plugins and agent teams. The difference that survives is defaults. Minimal harnesses ship small defaults and let users add; batteries-included harnesses ship the workflow.

### Axis G. Spec-first vs conversational

Kiro and HumanLayer at one end (review the plan, not the code); Böckeler's critique and Amp's "Steer, Don't Queue" (Sep 8, 2026) at the other; plan mode in nearly every harness in the middle. See §1.6.

### Axis H. Is the harness the moat?

| "The model is the product" | "The harness is the product" |
|---|---|
| Cherny: "never bet against the model"; scaffolding gains "wiped out with the next model" [E] | GitHub (Jun 25, 2026): "the harness shapes how effectively that intelligence is applied" [P\*, `round5-copilot-architecture.md`] |
| Amp: "the agent ... is no longer the limiting factor" [P] | Microsoft (Oct 28, 2026): "Improve the harness, and every surface it touches benefits." [P\*] |
| Amp: "The differences between frontier models are now small." [P] (so the harness is also not the moat; context and review are) | OpenAI (Aug 19, 2026): "Harness design can materially change results" [P, `round5-openai-codex.md`] |

[O] Both camps are acting on the same fact. If harness code goes stale with each model, the durable assets are elsewhere: the model (labs), the distribution and governance layer (GitHub, JetBrains), the codebase's own guides and sensors (Hashimoto, OpenAI, Böckeler), and the review workflow (Amp, JetBrains, Cognition's Devin Review). Vendors without their own model are buying or training one (Cursor, Cognition) or going model-agnostic and selling the rest (JetBrains, Amp, OpenCode).

---

## 3. Direction: what measurably shifted in 2026

### 3.1 Adoption and usage data

**JetBrains Developer Ecosystem Survey 2026** (fieldwork May to July 2026, "more than 15,000 professional developers", reweighted by region, employment, language and JetBrains familiarity) [P], https://blog.jetbrains.com/research/2026/08/ai-coding-agent-adoption-2026/ (published Aug 19, 2026 per page metadata; every figure in the table below re-checked against the raw page on 2026-11-04):

| Measure | Jan 2026 | May-Jul 2026 |
|---|---|---|
| Use coding agents at work weekly / daily | | 90% / 68% |
| Claude Code, used at work | 18% | 39% (US 47%); most-used tool for 31% |
| GitHub Copilot, used at work | 29% "a year ago" | 21%; awareness 79% |
| Codex, used at work | 3% | 16%; awareness 27% to 65% |
| Cursor, used at work | 18% | 12% |
| OpenCode | | 7% (awareness 42%) |
| Google Antigravity | | 6% (India 15%) |
| JetBrains AI / Junie | | ~9% |

- [P] "Claude Code ... is used twice as often as GitHub Copilot, a former long-standing leader of the market".
- [P] Code share, Aug 26, 2026 (same survey, self-reported, bucketed): "~47% of their code is fully written by agents", "~38% is written with some AI assistance", "~27% is written fully manually" (sums exceed 100% because of bucket midpoints, as JetBrains notes). "one in five writes literally zero code without AI". "Over 80% agent-generated code" is "a minority of around 22%". Seniors hand over more than juniors. C and C++ developers are the least agentic. East Asia about 32-35% heavy agent users vs about 16% in Europe and the UK. https://blog.jetbrains.com/research/2026/08/how-much-code-do-developers-really-let-agents-write/
- [R] A search summary we received claimed the "Claude Code 39%" figure was a misreading of "39% of GitHub Copilot users use it in JetBrains IDEs". Both numbers are on the JetBrains page and both are 39%. Claude Code at 39% adoption is correct.

**Stack Overflow Developer Survey 2026** ("More than 30K technologists from 169 countries"; the landing page counts 30,903 responses; published about early October 2026 per secondary coverage) [P], https://survey.stackoverflow.co/2026/ai:

- Coding assistants and agents are the top AI use case (66%), ahead of chatbots (63%); 73% use them daily; 31% of daily users spend 4+ hours a day.
- Coding agents used (question: "Have you used any of the following coding agents or assistants in the past year?"; n = 12,255 respondents to that question, so "among respondents who answered the coding-agent question", not strictly "among coding-agent users"): Claude Code 65.5%, GitHub Copilot 58.7%, OpenAI Codex 29.5%, Cursor 25.5%, Google Antigravity 16.0%, Gemini Code Assist 14.6%, OpenCode 13.6%, JetBrains AI 12.8%, Windsurf 6.5%, Warp 5.2%, Cline 4.5%, Pi 4.4%, Amazon Q Developer 3.9%. https://survey.stackoverflow.co/2026/ai/data
- Why people switched tools in the past year: better output quality 25.1%, employer required it 10.6%, lower cost 6.4%; 33.7% did not switch.
- [O] SO respondents skew toward heavy users and the question allows several answers, so SO overstates every tool relative to JetBrains. Both surveys agree on the order at the top: Claude Code first, Copilot second, Codex third.

**GitHub Octoverse 2026** (Oct 28, 2026; 12 months to Sep 30, 2026) [P], https://github.blog/news-insights/octoverse/octoverse-commits-pushes-reach-new-highs-in-2026-as-developers-build-with-agents/:

- "By September 2026, more than 40% of pull requests on GitHub started with an agent's first draft, up from 17% in March. That is 110 million in September alone, about 6x March's volume."
- Agent PRs merged within two weeks: 83% (Feb) to 90% (Sep), vs about 86% for PRs without detected agent involvement.
- "Among GitHub Copilot's monthly active users, 55% now use agentic features, up from 35% a year ago." "Copilot cloud agent ... grew 230% year over year, against 85% for agent chat."
- Merged PRs "more than tripled to 1.3 billion" (the comparison is with two years earlier, not one); commits 34.3 billion; "more than 225 million" developers.
- "Agents moved from single-session tools to persistent ones that could track progress across days and orchestrate other specialized agents. Just as important, agents began making extensive use of the cloud".
- Repos with an agent config file logged "eight times as many commits" as new repos without one. [O] Correlation; heavy users both write AGENTS.md files and commit more.

**METR** [P]:

- Feb 24, 2026 (older than 6 months): the 2025 RCT found AI made tasks take "19% longer" (CI +2% to +39%). The late-2025 rerun estimated -18% (speedup) for returning developers (CI -38% to +9%) and -4% for new recruits (CI -15% to +9%), but METR calls the data "an unreliable signal" because "developers choosing not to participate in the study because they do not wish to work without AI", "30% to 50% of developers told us that they were choosing not to submit some tasks", pay fell from $150/hr to $50/hr, and time tracking broke "for the fraction of developers who use multiple AI agents concurrently." METR: "we believe it is likely that developers are more sped up from AI tools now". https://metr.org/blog/2026-02-24-uplift-update/
- May 11, 2026: survey of 349 technical workers (87 software engineers), Feb-Apr 2026. "Participants self-reported a median 1.4–2x change in the value in their work due to AI tools. The median self-reported speed change ... is 3x." Retrospective 1.3x (Mar 2025), 2x (Mar 2026), forecast 2.5x (Mar 2027). "METR staff give the lowest change in value answers of any subgroup we study." "survey results are not necessarily grounded in reality"; their 2025 study found people "overestimated AI's effect on their time spent on tasks by 40 percentage points on average." https://metr.org/blog/2026-05-11-ai-usage-survey/
- [R] "METR reversed its finding and now shows AI makes developers 18% faster": METR says the estimate is unreliable and likely a lower bound; it did not publish a corrected headline number. METR's blog index shows no newer productivity study up to Nov 4, 2026.

**Revenue and run-rate** (company claims; run-rate is not recognised revenue):

| Company | Figure | Date | Tag |
|---|---|---|---|
| Anthropic (Claude Code) | "Claude Code's run-rate revenue has grown to over $2.5 billion; this figure has more than doubled since the beginning of 2026. The number of weekly active Claude Code users has also doubled since January 1." Enterprise use is "over half of all Claude Code revenue". Company run-rate $14B. | Feb 12, 2026 (older than 6 months) | [P] anthropic.com/news/anthropic-raises-30-billion-series-g-funding-380-billion-post-money-valuation |
| Cursor | "Cursor Recurring Revenue Doubles in Three Months to $2 Billion" | Mar 2, 2026 | [S] Bloomberg headline linked from Cursor's press list |
| Cognition | $1B annualized run rate | Sep 25, 2026 | [P] `round5-cursor-cognition.md` |
| Cursor sale price | $60B all-stock to SpaceX | announced Jun 2026, closed Aug 14, 2026 | [S] price (Techzine and others); [P] closing, cursor.com/blog/joining-spacex (Cursor's own post says the process "started in April", which sits awkwardly with the "Jun 2026" announcement date; not resolved) |

- [O] No primary 2026 Claude Code or Codex user count beyond these was found; sibling files reach the same conclusion.

### 3.2 Background and cloud agents became the growth surface

- [P] Octoverse: cloud agent +230% YoY; 40% of PRs agent-started (above).
- [P] Cursor: 35% of its internally merged PRs from autonomous cloud agents (Feb 26, 2026); cloud agents on customer-managed machines (Sep 2, 2026) [P, cursor.com/blog index].
- [P] Amp: "Agents in Orbs Run agents remotely" (Jun 30, 2026); "Self-Hosted Orbs" (Oct 22, 2026); runners on your own Mac (Sep 24, 2026); "Assign It To Amp" from Linear (Oct 19, 2026). https://ampcode.com/news
- [P] Codex Cloud, Copilot cloud agent, Kiro Web (GA Sep 3, 2026), Antigravity remote agents (rolling out Nov 3, 2026), Devin: see sibling files. Google shut Jules on Oct 29, 2026 and moved remote agents into Antigravity [P, `round5-google-amazon-jetbrains.md`].
- [O] Self-hosted runners are the 2026 enterprise answer to "someone else's computer". Cursor, Amp and Copilot all now let the cloud agent run on machines the customer controls.

### 3.3 Agent inboxes and manager views

| Product | Date | Tag |
|---|---|---|
| Cursor 3 Agents Window ("All local and cloud agents appear in the sidebar") | Apr 2, 2026 | [P] |
| Devin Desktop replaces the Windsurf brand ("agent command center", ACP third-party agents) | Jun 2, 2026 | [P] blog index; detail in `round5-cursor-cognition.md` |
| Amp Puck, a meta-agent you can talk to by voice to control your agents | Jul 20 and Aug 18, 2026 | [P] ampcode.com/news |
| JetBrains Air (multi-agent environment) and JetBrains Central (control plane) | Air introduced Sep 22, 2026 | [P] JetBrains blog |
| GitHub Copilot app, Agent HQ / VS Code agent sessions | see `round5-copilot-architecture.md` | [P] |
| Antigravity Agent Manager, to be removed from the IDE "in an upcoming release" | stated 2026 | [P] `round5-google-amazon-jetbrains.md` |

[O] The manager view is converging on the same objects: a list of sessions, each local or cloud, each with a diff or artifact to review, movable between machine and cloud. Google removing its Agent Manager from the IDE is the one counter-signal; it is moving that function to the standalone app, not dropping it.

### 3.4 Long-running loops became a product feature

- Ralph (Jul 2025) to Anthropic's `ralph-loop` plugin (Jan 2026) to `/goal` modes in Codex, Claude Code and Cursor (May to Aug 2026), plus self-scheduling agents in Amp (Jul 21, 2026) and Devin ("Devin can now Schedule Devins", Mar 20, 2026) [P, blog indexes]. See §1.5.
- [P\*] Cursor, Sep 23, 2026: "Improved token efficiency for longer agent runs" (cursor.com/blog index). [S] Pi Durable for long-running agents (`round5-oss-terminal.md`).

### 3.5 Harness makers train their own models

| Harness | Own model(s), 2026 | Tag |
|---|---|---|
| Cursor | Composer 2 (Mar 19), 2.5 (May 18), then Grok 4.6/4.7 "with SpaceXAI" (Aug/Sep). "Grok 4.6, which we released Wednesday" is "an early look at what we can now build together." | [P] `round5-cursor-cognition.md`; [P] joining-spacex |
| Cognition | SWE-1.6 (Apr), SWE-1.7 (Jul), SWE-2 (Sep 10), SWE-2 Flash (Nov 4) | [P] blog index |
| GitHub Copilot | own fine-tuned models and Fusion multi-model routing (GA at Universe, Oct 28) | [P] `round5-copilot-architecture.md`; Octoverse |
| JetBrains | Junie Local runs a Qwen model JetBrains "chose and tuned" against its agent loop | [P\*] `round5-google-amazon-jetbrains.md` |
| Labs (inverse direction) | OpenAI tunes per-model harness settings in data; Anthropic ablates the Claude Code prompt per model | [P] sibling files |

[O] Two routes to the same coupling: labs ship harnesses tuned to their models, and harness makers ship models tuned to their harness. The model-agnostic camp (JetBrains, Amp, OpenCode, Goose, Pi) is the group without a model of its own.

### 3.6 Consolidation, Jul 2025 to Nov 2026

| Event | Date | Tag |
|---|---|---|
| Cognition acquires Windsurf product, IP and brand | Jul 14, 2025 (older than 6 months) | [P] `round5-cursor-cognition.md` |
| Pi moves to Earendil | Apr 8, 2026 | [P] `round5-oss-terminal.md` |
| SpaceX agrees to buy Cursor (Anysphere) for $60B all-stock | Jun 2026 | [S] Techzine and others |
| Gemini CLI restricted to paid enterprise use; successor Antigravity CLI | Jun 18, 2026 | [P] `round5-google-amazon-jetbrains.md` |
| Cursor acquisition by SpaceX closes ("completes the acquisition process that started in April") | Aug 14, 2026 | [P] |
| Kimi CLI (Python) archived for Kimi Code CLI | last push Sep 22, 2026 | [P] `round5-oss-terminal.md` |
| Jules turned down | Oct 29, 2026 | [P] `round5-google-amazon-jetbrains.md` |
| Amazon Q Developer end-of-support plan; Kiro is the successor | Apr 30, 2026 | [P] `round5-google-amazon-jetbrains.md` |
| Aider: last release Feb 12, 2026, last merge May 22, 2026 | | [P] `round5-oss-terminal.md` |

### 3.7 Protocol convergence

- AGENTS.md and MCP went to the Linux Foundation's Agentic AI Foundation (Dec 9, 2025) [P, `round5-openai-codex.md`]; Agent Skills (`SKILL.md`) read by Claude Code, Copilot and most open-source agents [P, sibling files]; ACP used by JetBrains, Zed, Devin Desktop, Cursor (`agent acp`), Copilot CLI and Goose [P, sibling files]; VS Code's MIT-licensed Agent Host Protocol (Aug 26, 2026) [P\*, `round5-copilot-architecture.md`].
- [P] Exception: Claude Code docs and changelog do not mention ACP (`round5-claude-code.md`).
- [O] The protocols standardise the edges (instructions, skills, tools, the UI connection). None standardises the loop, the prompt or context management, which is where vendors still compete.

### 3.8 What builders say is next (stated only)

- [P] Amp, Feb 19, 2026: "Today Amp ceases to be a coding agent. It's no longer a point on a map. It's an arrow." The CLI is "a ladder: we use it to climb up to the next level and then we might not need it."
- [P] Cursor: "We will also continue to invest in the IDE until codebases are self-driving." (Apr 2, 2026); from-scratch SpaceXAI model expected (May 18, 2026, `round5-cursor-cognition.md`).
- [P] Cognition, Sep 8, 2026: "agents will become proactive by default, software will improve itself" (`round5-cursor-cognition.md`). Yan, Apr 2026: the open problems "are all communication problems."
- [P\*] (openai.com 403; not re-seen) OpenAI harness team, Feb 2026: "We're still learning where human judgment adds the most leverage and how to encode that judgment so it compounds."
- [P] Böckeler, Apr 2026: "We need a way to evaluate harness coverage and quality similar to what code coverage and mutation testing do for tests."
- [P] JetBrains, Sep 22, 2026: "Standardizing on one AI vendor today means making a multi-year commitment in a market that won't look the same next quarter."
- [P] Microsoft/GitHub, Oct 28, 2026: one unified Copilot harness across surfaces, while "you can continue to bring in any harness and framework you want" (`round5-copilot-architecture.md`).

---

## 4. Refuted or risky wording [R]

- "OpenAI coined 'harness engineering'." Hashimoto used it on Feb 5, 2026; OpenAI's post is Feb 11 (§1.7).
- "Three OpenAI engineers wrote a million lines with AI." Three engineers drove the first ~1,500 PRs, the team grew to seven, Codex wrote all code (§1.7).
- "Cognition says never build multi-agent systems." Its CPO (Walden Yan; title from secondary sources [S], the posts give only his name) revised the position in April 2026 to single-threaded writes plus helper agents (§1.4).
- "Anthropic proved multi-agent beats single-agent by 90%." The 90.2% is on Anthropic's internal research eval, and the same post says most coding tasks are a poor fit (§1.4).
- "Cursor proved semantic search beats grep." Cursor turned embeddings off in July 2026 (§1.2).
- "METR now shows an 18% speedup." METR calls the estimate unreliable (§3.1).
- "Copilot is still the most used coding tool." JetBrains and SO 2026 both put Claude Code first among professional developers; Copilot remains the most widely known (79% awareness, JetBrains).
- Karpathy "less Iron Man robots and more Iron Man suits" is genuine wording from the June 2025 talk transcript, but it predates his Feb 2026 "basically work since" December comment. Show both with dates.
- "Pi will never support MCP" (see `round5-oss-terminal.md`).
- Amp "watch your agents work step-by-step, you're giving them too short a leash." The sentence on the page has no "step-by-step" (§1.5).
- Cursor swarm "typically peaked at several hundred agents" and "a small, steady error rate": both non-verbatim. Use "most runs would peak at several hundred agents" and "The error rate remains small and constant" (§1.4).

## 5. Notes for the presentation [O]

1. **One timeline slide carries the philosophy section.** Jun 2025: Karpathy "keep the AI on the leash"; Cognition "Don't Build Multi-Agents"; Anthropic multi-agent research. Feb 2026: Karpathy "basically work since" December; Hashimoto names harness engineering; OpenAI "Humans steer. Agents execute."; Amp "The coding agent is dead". Apr 2026: Cognition's revision; Böckeler's guides and sensors. Jul to Sep 2026: Cursor drops embeddings; Amp swaps models with no complaints; Amp "too short a leash".
2. **Best three quotes for a bank audience:** Böckeler's "Guides (feedforward controls)" / "Sensors (feedback controls)" (maps to preventive and detective controls); JetBrains' "Code becomes cheaper to generate but more expensive to verify."; Yan's "writes stay single-threaded".
3. **The data slide:** JetBrains 90% weekly / 68% daily and Octoverse "more than 40% of pull requests" agent-started, next to METR's warning that self-reports are "not necessarily grounded in reality". That pairing is honest and lands with engineers.
4. **For a Copilot-only shop:** the axes show Copilot sits in the multi-model, one-harness-every-surface, keep-an-index, governance-first corner. The patterns that travel regardless of tool are the ones every camp agrees on: short AGENTS.md as a map, plan before code, one writer with read-only helpers, a clean-context reviewer, deterministic sensors (tests, types, linters, hooks), and fixing the harness each time the agent repeats a mistake (Hashimoto's definition).
5. **Avoid on slides:** run-rate numbers without "company claim, run-rate", Gas Town as a recommendation (its author says "You probably don't want to use it yet"), and any single-benchmark harness comparison.
6. **Westpac.** Amp Labs announced an on-site partnership with Westpac on Jul 29, 2026 [P]. It is the only bank-specific harness deployment we found stated by a vendor; useful as a peer reference, not as evidence of results (the post reports none).

## 6. Open questions

- Karpathy's original "agentic engineering" post (date and wording): X was not readable; only secondary coverage.
- No Claude Code-specific run-rate after Feb 12, 2026 on a primary page.
- Cursor's $2B revenue is a Bloomberg headline we did not read. No primary Codex user count.
- ~~Stack Overflow's exact question wording for the coding-agent list was not visible in the reader output; the denominator is inferred from counts.~~ Resolved 2026-11-04: "Have you used any of the following coding agents or assistants in the past year?", n = 12,255.
- No 2026 DORA report with agent-specific findings was found on a primary page; secondary coverage cites a DORA "ROI of AI-Assisted Software Development" study with conflicting dates.
- Whether Copilot will follow Cursor in dropping its semantic index: nothing stated.
- METR has announced a redesigned productivity study but published no results as of Nov 4, 2026.

## Verification pass (2026-11-04)

Method: raw HTML downloaded with curl and stripped to text, then each quote and number searched as an exact string. A [P] after this pass means the string was found on the primary page's raw text. Where the primary page blocked us, the tag is [P\*] or the item is listed under "could not verify".

**Headline claims checked against the primary page**

1. JetBrains DevEco 2026: confirmed [P]. 15,000+ devs, May to July 2026, 90% weekly / 68% daily, Claude Code 39% (18% in Jan, US 47%, main tool for 31%), Copilot 21% (29% "a year ago", awareness 79%), Codex 16% (3% in Jan, awareness 27% to 65%), Cursor 12% (18% in Jan), OpenCode 7%, Antigravity 6%, JetBrains AI ~9%. Post dated Aug 19, 2026 in page metadata.
2. Stack Overflow 2026: confirmed [P]. 65.5 / 58.7 / 29.5 / 25.5 match the data table (8,030 / 7,196 / 3,620 / 3,127 of n = 12,255). Wording fix: the base is everyone who answered "Have you used any of the following coding agents or assistants in the past year?", not "coding-agent users". 30,903 total responses, 169 countries.
3. Octoverse 2026 (Oct 28, 2026): confirmed [P]. "more than 40%", "up from 17% in March", "110 million", Copilot cloud agent "grew 230% year over year, against 85% for agent chat". Minor fix: merged PRs "more than tripled" over two years.
4. METR Feb 24, 2026: confirmed [P]. "an unreliable signal", "do not wish to work without AI", "30% to 50% of developers", pay cut $150 to $50/hr, and "likely that our estimate reported above is a lower-bound". The rerun started in August 2025.
5. METR May 11, 2026: confirmed [P]. 349 workers (87 software engineers), Feb to Apr 2026, median 1.4 to 2x value, 3x speed, "not necessarily grounded in reality", "40 percentage points".
6. Hashimoto "harness engineering": confirmed [P]. Post dated February 5, 2026; exact sentence present. The "six days before OpenAI" depends on OpenAI's Feb 11 date, which is corroborated by Böckeler's memo (Feb 17) and mirrors but not seen on openai.com.
7. OpenAI harness-engineering numbers: not re-seen on the primary page (openai.com returned 403 to curl and WebFetch; the reader-proxy route was blocked in this session). Downgraded from [P] to [P\*]. Corroboration: exact-phrase search matches "roughly 1,500 pull requests have been opened and merged with a small team of just three engineers driving Codex" on several mirrors; Böckeler's memo independently says "over 1 million lines of code"; the ~100-line AGENTS.md as a map is consistent across several secondary write-ups.
8. Cognition Apr 22, 2026: confirmed [P]. Byline Walden Yan, dated 2026.04.22; "multiple agents contribute intelligence to a task while writes stay single-threaded", map-reduce-and-manage, swarm "mostly a distraction", "communication problems" all verbatim. Also confirmed: "Our original observations still hold today for parallel-writer swarms". Yan's CPO title is not on either post [S].
9. Cursor embeddings reversal: confirmed [P] on the forum thread JSON. Maxime (staff) Jul 21: "grep / indexed search", "rapidly no longer helping"; Colin (staff) Jul 22: "turned down in favor of grep-based retrieval"; Mohit (staff) Jul 31: "no embeddings involved anywhere in it". Cursor semsearch post dated Nov 6, 2025 with the 12.5% (6.5% to 23.5%) figure.
10. Amp "Who Cares About the Model?" (Jul 29, 2026): confirmed [P]. All three quotes verbatim. Added context: Claude Opus 4.8 to GPT-5.6 Sol via the Dial, and the next line "But they still matter to us".
11. Amp "The Coding Agent Is Dead": confirmed [P]. Post dated Feb 19, 2026; extensions "self-destruct on March 5 at 8pm Pacific Time"; "no longer the limiting factor" verbatim.
12. Anthropic Series G (Feb 12, 2026): confirmed [P]. "over $2.5 billion", "more than doubled since the beginning of 2026", weekly actives doubled since Jan 1, enterprise "over half of all Claude Code revenue", company run-rate $14 billion.

**Corrections made**

- Amp Sep 25, 2026 quote: "watch your agents work step-by-step, you're giving them too short a leash" corrected to "watch your agents work, you're giving them too short a leash" (short version, §1.5; added to §4).
- Cursor "Towards self-driving codebases": "typically peaked at several hundred agents" corrected to "most runs would peak at several hundred agents"; "a small, steady error rate" was a paraphrase in quote marks, replaced with the page's wording (§1.4; added to §4).
- OpenAI harness-engineering and Codex-launch claims: [P] to [P\*] (not re-seen; see item 7). The earlier note telling `round5-openai-codex.md` to upgrade to [P] was softened accordingly.
- Octoverse "Merged PRs tripled" changed to "more than tripled" with the two-year baseline.
- SO base described precisely; open question on SO wording closed.

**Spot-checks beyond the headline list (all confirmed verbatim on the raw page, tag raised [P\*] to [P] unless noted)**

Anthropic "Building effective agents" (Dec 19, 2024) both quotes; Anthropic multi-agent research post (Jun 13, 2025): 90.2%, "about 15× more tokens than chats", "80% of the variance", the coding caveat; Thorsten Ball (Apr 15, 2025) "an LLM, a loop, and enough tokens", "less than 400 lines of code"; Willison Sep 18, Jun 16, Sep 30, Oct 5 2025 and Feb 23 2026 quotes; Karpathy Feb 2026 and Oct 2025 wording as quoted on Willison's pages (kept [P\*] because the originals are a tweet and a podcast); Cognition Jun 12, 2025 principles; Aider repo-map and unified-diff posts (20% to 61%, the four principles); Cline (Nick Baumann, May 27, 2025) three quotes; HumanLayer 12-Factor list and ACE quotes; Huntley "Ralph" (14 Jul 2025) four quotes; Anthropic `ralph-loop` README "Stop hook" wording; Cursor "third era" (Feb 26, 2026; "Thirty-five percent", "2x as many agent users as Tab users"); Cursor 3 (three quotes); Cursor joining SpaceX (Aug 14, 2026; "started in April", Grok 4.6 line); LangChain (Vivek Trivedy, March 10, 2026) all quotes incl. Terminal-Bench 2.0 line; Böckeler memo (17 February 2026), harness article (02 April 2026) and SDD article (15 October 2025), every quote; JetBrains code-share post (Aug 26, 2026) ~47 / ~38 / ~27%, "one in five", "around 22%"; Octoverse 61% multi-model and "no single model carried more than 25%"; Amp news index items (Jul 17 agent-to-agent, Jul 21 schedules, Jun 30 Orbs, Oct 22 Self-Hosted Orbs, Oct 19 Linear, Jul 29 Westpac, Sep 8 Steer Don't Queue, Puck Jul 20).

**Could not verify this pass**

- openai.com pages (harness engineering, Codex launch, unrolling the Codex agent loop): 403.
- Steve Yegge "Welcome to Gas Town" on Medium: 403 to curl and WebFetch. Quotes left as written, flagged [P\*].
- Karpathy original tweet and "agentic engineering" post (X not readable); YC and Cherny transcripts remain [E].
- Sibling-file claims (Kiro, Copilot, Claude Code, Cognition revenue, Pi) were not re-checked here; they keep the sibling file's tag.
- Cursor $60B price and "announced Jun 2026": secondary only; Cursor's own closing post says the process "started in April".
