---
url: https://arxiv.org/abs/2506.12286, https://arxiv.org/abs/2410.06992, https://epoch.ai/publications/what-skills-does-swe-bench-verified-evaluate, https://www.latent.space/p/swe-bench-dead, https://news.ycombinator.com/item?id=47910388, https://metr.org/blog/2026-1-29-time-horizon-1-1/
fetched: 2026-08-12
---

# Track 3 — Critiques of the Coding Benchmarks (August 2026)

Companion to track3-benchmarks.md. Each critique carries its citation URL.

---

## 1. Contamination: the benchmark is in the training data

- SWE-bench Verified's 500 tasks all come from **public GitHub repos that predate every frontier model's training cutoff**; roughly half the issues predate 2020 — https://epoch.ai/publications/what-skills-does-swe-bench-verified-evaluate
- **SWE-bench+** (arXiv:2410.06992): audit of original SWE-bench found **32.67% of "successful" patches involved solution leakage** — the fix was literally in the issue report or its comments; **31.08% of passed patches were "suspicious"** — accepted only because the test suite was too weak to catch incorrect/incomplete patches. After filtering, SWE-Agent+GPT-4's resolve rate fell **12.47% → 3.97%**. Over **94% of issues predate LLM knowledge cutoffs**. Same defects present in Lite and Verified — https://arxiv.org/abs/2410.06992
- Smoking gun (2026): OpenAI's Frontier Evals team reported that frontier models could **reproduce gold-patch solutions verbatim given only the task ID**, and GPT-5.2's chain-of-thought contained implementation details never stated in the problem — https://www.latent.space/p/swe-bench-dead
- LiveCodeBench exists precisely because of this failure mode: it dates every problem and scores models only on problems released after their cutoff — https://livecodebench.github.io/

## 2. The "SWE-Bench Illusion" paper (arXiv:2506.12286)

"The SWE-Bench Illusion: When State-of-the-Art LLMs Remember Instead of Reason" — Liang (Purdue), Garg, Zilouchian Moghaddam (Microsoft) — https://arxiv.org/abs/2506.12286 , https://www.microsoft.com/en-us/research/publication/the-swe-bench-illusion-when-state-of-the-art-llms-remember-instead-of-reason/

- Diagnostic 1 — **file-path identification**: given only the issue text, no repository access at all, SOTA models identify the buggy file path with **up to 76% accuracy** on SWE-bench Verified tasks. On issues from repos NOT in SWE-bench, this drops to **up to 53%** — a 23-point in-distribution vs out-of-distribution gap that only memorization explains.
- Diagnostic 2 — **function reproduction**: models emit **up to 35% consecutive-5-gram verbatim matches** of ground-truth code on SWE-bench Verified/Full vs only **up to 18%** on other benchmarks — they are partially reciting the gold patch.
- Conclusion: Verified scores are inflated by memorization and "do not purely reflect a model's transferable software engineering skills"; contamination-resistant benchmarks are needed.

## 3. Realism: GitHub issues != real dev work

All from Epoch AI's task-level analysis — https://epoch.ai/publications/what-skills-does-swe-bench-verified-evaluate — unless noted:

- **Repo concentration**: only 12 Python repos; 5 repos account for >80% of tasks; **Django alone is ~half the benchmark**. It is a Python-monoculture benchmark scoring "general" coding ability (see also https://agentmarketcap.ai/blog/2026/04/06/aider-polyglot-leaderboard-2026-swe-bench-python-bias).
- **Task-type skew**: 87% bug fixes, 9% feature work, 4% refactoring. No design, no ambiguity resolution, no cross-service work, no code review.
- **Task-size skew**: ~90% of tasks are completable in under an hour by a human; **39% are "trivial" (<15 min)**. "Long-horizon coding" claims built on Verified rest mostly on short tasks.
- **Issue-text quality**: the Verified effort itself found 38.3% of original SWE-bench problem statements underspecified — real issues are messy, and curating them away also curates away realism — https://openai.com/index/introducing-swe-bench-verified/ (details mirrored at https://github.com/irthomasthomas/undecidability/issues/933).
- **Tests as ground truth are unreliable**: OpenAI's 2026 audit of 138 problematic Verified tasks: **>60% unsolvable as written** — 49 tests too narrowly defined (reject correct solutions), 26 demanded undisclosed features — https://www.latent.space/p/swe-bench-dead . An ICSE 2026 empirical study asks directly whether "solved" SWE-bench issues are solved correctly and finds many plausible-but-wrong patches pass — https://software-lab.org/publications/icse2026_SWE-bench-correctness.pdf

## 4. Saturation: what >90% means

- Frontier cluster as of Aug 2026: 95–96% at the top (Opus 5 96.0%, Mythos 5 95.5%, Fable 5 95.0% — vendor-reported), with a dense 80–89% band below — https://benchlm.ai/benchmarks/sweVerified . Within-cluster differences are smaller than harness effects, so ranks are noise.
- **OpenAI stopped reporting Verified in early 2026** ("The End of SWE-Bench Verified," Latent Space, Feb 23, 2026, with OpenAI Frontier Evals VP Mia Glaese and researcher Olivia Watkins): plateau ~80%+ leaves "minimal room for meaningful differentiation," and the residual unsolved tail is dominated by broken tasks, not hard engineering — https://www.latent.space/p/swe-bench-dead
- Reality check: the same models that score 95% on Verified score **46–61% on Scale's standardized SWE-bench Pro board** — the gap between a saturated, contaminated benchmark and a fresher one is 35+ points — https://labs.scale.com/leaderboard/swe_bench_pro_public , https://agentmarketcap.ai/blog/2026/04/10/swe-bench-saturation-90-percent-coding-benchmarks
- HN discourse on the announcement: "You can't trust that a model that scores 93% is better... at that point it's impossible to distinguish between recall and reasoning" — https://news.ycombinator.com/item?id=47910388

## 5. "Benchmarks vs vibes"

- Practitioner discourse has shifted to private, hands-on evaluation. Representative HN sentiments (thread on OpenAI dropping Verified): distrust of vendor-reported numbers ("you never know when you get the nerfed session"), and "let the model speak for itself" via private evals since public benchmarks are inherently compromised once they matter — https://news.ycombinator.com/item?id=47910388
- Simon Willison's line of argument: distinguishes irresponsible "vibe coding" from disciplined "vibe engineering," but consistently evaluates models by working with them on real tasks (his pelican-on-a-bicycle-style personal probes) rather than by leaderboard position — https://simonwillison.net/2025/Mar/19/vibe-coding/ , https://simonwillison.net/2025/Oct/7/vibe-engineering/
- The advice that circulates in 2026 practitioner writing: "look at the benchmarks, but trust your vibes. If a model feels like it's fighting you, it is, no matter what the MMLU says" — https://aidevdayindia.org/blogs/interpreting-llm-benchmark-scores/vibe-coding-vs-benchmarks.html
- The vibes are backed by data: on **Vibe Code Bench** (build a whole working web app from a spec, graded by 964 browser workflows), the best models manage only **46% (Opus 4.6) and 42% (GPT-5.2) Pass@1** — models that "solve" 80–95% of Verified fail most end-to-end app builds — https://arxiv.org/abs/2603.04601

## 6. METR time horizons as the alternative paradigm

- Instead of a static pass rate on a fixed set, METR measures **the length of task (human-expert time) an agent can finish at 50% reliability**, fitting a curve over tasks from seconds to 8+ hours. This yields a longitudinal, saturation-resistant metric: the 50% horizon has doubled every ~7 months since 2019 (196.5-day full-trend estimate), accelerating to **~131 days since 2023 and ~89 days since 2024** under the TH1.1 suite (228 tasks, Jan 2026) — https://metr.org/blog/2026-1-29-time-horizon-1-1/ , https://metr.org/blog/2025-03-19-measuring-ai-ability-to-complete-long-tasks/ , https://metr.org/time-horizons/
- Its own honest caveats: measurements above 16 hours are unreliable with the current suite; only 5 of the 31 long tasks have real human baselines (the rest use estimates); CIs understate run-level variance — https://metr.org/blog/2026-1-29-time-horizon-1-1/ , https://metr.org/time-horizons/
- Why presenters like it: it answers "what can I delegate?" (a task-length question) rather than "what fraction of a frozen dataset passes?" — and it keeps discriminating after pass-rate benchmarks saturate.

## 7. Scaffold-dependence breaks comparability

- Same model, different harness, different score: GPT-4o 23% → 33.2%; Claude 3.7 62.3% → 70.2%; DeepSeek R1-0528 33% → 57.6% (+24.6 pp) — https://epoch.ai/publications/what-skills-does-swe-bench-verified-evaluate . Epoch's verdict: "results with one scaffold often do not transfer to another scaffold," so cross-vendor leaderboard rows are not comparable measurements.
- Terminal-Bench makes this visible on one page: Claude Fable 5 scores 83.8% under Claude Code but 80.4% under the reference Terminus 2 agent; Gemini 3 Pro scores 73.9% (Terminus 2) vs 65.8% (Gemini CLI) — https://www.tbench.ai/leaderboard/terminal-bench/2.1
- Harness choices (tools exposed, retries, context management, token/turn budgets, test-time compute) move SWE-bench-family scores by **5–20 points**; an Opus 4.5 run varied 50.2%–55.4% on SWE-bench Pro across three harnesses with the model held constant — https://www.digitalapplied.com/blog/swe-bench-verified-june-2026-benchmark-vs-scaffolding-analysis , https://www.futureagi.com/blog/coding-agent-harness-benchmark/

## 8. Self-reported vendor scores vs independent reproduction

- **99 of 100** SWE-bench Verified scores on a major tracker were vendor-submitted with no independent verification (June 2026 snapshot) — https://www.digitalapplied.com/blog/swe-bench-verified-june-2026-benchmark-vs-scaffolding-analysis
- **Epoch AI runs its own standardized SWE-bench Verified harness** (simple agent loop; bash/text_editor/apply_patch; re-evaluated under v2.0 methodology Feb 2026) precisely because vendor numbers embed bespoke scaffolds and larger compute budgets; independent runs generally come in lower — https://epoch.ai/benchmarks/swe-bench-verified
- Standardized-vs-vendor deltas on SWE-bench Pro: Anthropic reports Opus 4.8 at 69.2% while Scale's SEAL standardized board puts the best Claude (Opus 4.6 thinking) at 51.9% (~17 pp); Anthropic reports Fable 5 at 80.0% / Opus 5 at 79.2% while neither model's SEAL-standardized equivalent appears near that on the public board (top standardized score: Muse Spark 1.1, 61.5%) — https://www.digitalapplied.com/blog/swe-bench-verified-june-2026-benchmark-vs-scaffolding-analysis , https://www.marktechpost.com/2026/07/24/meet-the-new-claude-opus-5-frontier-class-agentic-coding-and-computer-use-at-unchanged-opus-pricing/ , https://labs.scale.com/leaderboard/swe_bench_pro_public
- The confusion is now itself a story: "Three sources, three different SWE-bench Pro leaders" — contested scores depending on whether you read vendor cards, aggregators, or standardized boards — https://techjacksolutions.com/ai-brief/three-sources-three-different-swe-bench-pro-leaders-how-to-r/ , https://techjacksolutions.com/ai-brief/claude-fable-5s-swe-bench-pro-score-is-contested-what-indepe/
- Practical rule for the slide: **a benchmark score without (a) the harness, (b) who ran it, and (c) the compute/retry budget is marketing, not measurement.**

## Verification notes (honesty section)
- openai.com/index/introducing-swe-bench-verified/ blocked direct fetch (403); its creation-process numbers (93 developers, 1,699 annotated, 500 kept, 38.3%/61.1% defect rates, GPT-4o 16%→33.2%) were confirmed via mirrors quoting the post — https://github.com/irthomasthomas/undecidability/issues/933 , https://hyper.ai/en/datasets/33655
- The official swebench.com leaderboard rows could not be machine-extracted (JS-rendered); Aug 2026 Verified top scores cited here are vendor-reported figures via aggregator trackers (benchlm.ai, codesota.com, morphllm.com) and vendor announcements. I could not independently verify 96.0%/95.5%/95.0% beyond these sources.
- The reported "~12 hour" 50% time horizon for Claude Opus 4.6 comes from secondary summaries of METR's tracker; I could not extract the exact figure from metr.org's interactive chart. METR flags all >16 h measurements as unreliable.
