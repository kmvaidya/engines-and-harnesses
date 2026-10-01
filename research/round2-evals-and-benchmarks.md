---
url: https://anthropic.com/engineering/demystifying-evals-for-ai-agents, https://hal.cs.princeton.edu/corebench_hard, https://epoch.ai/benchmarks/swe-bench-verified, https://agentmarketcap.ai/blog/2026/04/12/scale-ai-seal-standardized-scaffold-swe-bench-rankings-2026, https://codex.danielvaughan.com/2026/06/17/benchmark-literacy-guide-reading-coding-agent-benchmarks-critically/, https://www-cdn.anthropic.com/bf10f64990cfda0ba858290be7b8cc6317685f47/Claude%20Opus%204.5%20System%20Card.pdf, https://labs.scale.com/leaderboard/swe_bench_pro_public, https://www.augmentcode.com/blog/auggie-tops-swe-bench-pro, https://www.morphllm.com/blog/warpgrep-v2, https://llm-stats.com/benchmarks/swe-bench-verified, https://blog.kilo.ai/p/kilobench-because-your-benchmark, https://www.tbench.ai/leaderboard, https://www.tbench.ai/news/terminal-bench-4-0, https://metr.org/time-horizons/, https://metr.org/assets/benchmark_results_1_1.yaml, https://metr.org/blog/2026-09-22-claude-opus-5-5/, https://metr.org/blog/2026-06-26-gpt-5-6-sol/, https://epoch.ai/benchmarks/mirrorcode, https://epoch.ai/data/benchmark_data.zip, https://www.swebench.com/, https://hal.cs.princeton.edu/, https://openai.com/index/introducing-gpt-5-4/, https://openai.com/index/introducing-gpt-5-3-codex/
fetched: 2026-09-30
---

# Agent evals and the harness effect on benchmarks

Round 2 file. Tags: **[V]** 3-agent adversarial check passed, **[S]** hand
spot-check, **[P]** confirmed against the primary source on 2026-09-30,
**[E]** extracted with quote but not cross-checked, **[R]** refuted.

**Coverage:** §6 (added in a follow-up pass, 2026-09-30) records what the
independent boards show for the GPT-6 / Fable 5 generation. In short:
Terminal-Bench is now version 4.0 and has several new models; SEAL, METR time
horizons, swebench.com and HAL have none; Epoch's MirrorCode has a few.

## 1. A score belongs to the model and the harness together [V]

- Anthropic, "Demystifying evals for AI agents" (Jan 9, 2026): "When we
  evaluate 'an agent,' we're evaluating the harness _and_ the model working
  together."
- **CORE-Bench example.** Opus 4.5 first scored 42%. An Anthropic researcher
  found "rigid grading that penalized '96.12' when expecting '96.124991…',
  ambiguous task specs, and stochastic tasks that were impossible to reproduce
  exactly. After fixing bugs and using a less constrained scaffold, Opus 4.5's
  score jumped to 95%."
- **Independent partial confirmation.** Princeton HAL declared CORE-Bench
  solved in Dec 2025 with Opus 4.5 on a Claude Code scaffold: 77.78% with
  automated grading, 95.5% after manual validation. So roughly 35+ points came
  from the scaffold and about 18 from grading.
- Caveat: part of the jump came from changing what was measured. Use it as one
  vivid example, not as a general "harness = +50 points" rule.

## 2. Building a first eval suite [P]

From the same Anthropic post (Mikaela Grace, Jeremy Hadfield, Rodrigo
Olivares, Jiri De Jonghe). All four quotes confirmed verbatim on 2026-09-30.

- Start small: "20-50 simple tasks drawn from real failures is a great start."
- Report **pass^k** (all k trials succeed) next to pass@k. "If your agent has
  a 75% per-trial success rate and you run 3 trials, the probability of
  passing all three is (0.75)³ ≈ 42%." For a bank, pass^k is closer to what
  reliability means.
- Grade the outcome, not the path: "It's often better to grade what the agent
  produced, not the path it took."
- Validate graders by reading transcripts: "You won't know if your graders are
  working well unless you read the transcripts and grades from many trials."

## 3. Independent evidence that the harness alone moves scores

- **Epoch AI v2.0.0 upgrade (Feb 12, 2026)** [P]. "We performed a major
  upgrade of scaffolding, environments, and token limits. We updated the
  Epoch version of this benchmark to v2.0.0, and re-evaluated key models.
  This led to model performance improving significantly. Our default graph
  view above only displays results from v2.0.0 onwards." Same models, so the
  gain is the harness.
- [P] Epoch runs 484 of 500 Verified tasks; the 16 excluded have problems
  like "tests that require network access, or repo versions that are
  incompatible." The exclusion barely matters: "GPT-5 Mini's results on the
  SWE-bench bash-only leaderboard would be 59.8% if they also excluded these
  issues, compared to a reported 59.9%". (Both figures are from the SWE-bench
  bash-only board, not Epoch's own runs.) So it does not explain
  vendor-vs-independent gaps.
- **Scale SEAL board** [P] (labs.scale.com/leaderboard/swe_bench_pro_public;
  scale.com redirects there). SWE-bench Pro public set, 731 instances:
  Opus 4.5 45.89±3.60, GPT-5 (High) 41.78±3.49, GPT-5.2 Codex 41.04±3.57.
  [R] "Every model gets the same SWE-Agent scaffold" no longer holds: most
  entries run "with an uncapped cost and with a turn limit of 250", greyed
  entries with a cost cap and 50 turns, and the asterisked top entries are
  "Run with mini-swe-agent harness". Current top: Muse Spark 1.1 61.50,
  GPT-5.4 (xHigh) 59.10, Muse Spark 55.00, Opus 4.6 (thinking) 51.90, Gemini
  3.1 Pro (thinking) 46.10; Opus 4.5 is sixth. The board shows no dates.
- Opus 4.5 on Verified is 80.9% [P], from the Opus 4.5 System Card (Table
  2.3.A); the launch post shows it only in a chart image. The same card gives
  Opus 4.5 **52.0% on SWE-bench Pro** under Anthropic's own setup, against
  45.89% on SEAL's board: a 6-point gap from the harness alone.
- **Same weights, different product harnesses** [P, corrected]. Augment
  Code, "Auggie tops SWE-bench Pro" (augmentcode.com/blog/auggie-tops-swe-bench-pro,
  Feb 4, 2026, updated Jun 18), 731 problems: Auggie + Opus 4.5 51.80%,
  Cursor + Opus 4.5 50.21%, Claude Code + Opus 4.5 49.75%, SWE-Agent + Opus
  4.5 45.89%. Spread across the three products: about 2 points (about 15
  problems); about 6 points if SWE-Agent is included. Augment is a vendor
  ranking its own product first. [R] Round 1's "50.2% to 55.4%" (in
  `track3-benchmarks.md` and `track3-benchmark-critiques.md`, from aggregator
  blogs) is wrong. 55.4% is Opus **4.6**'s baseline in Morph's WarpGrep post.
- **Lab-reported vs standardized on Pro** [P]. Read in full through a reader
  proxy and web.archive.org (openai.com refuses direct fetches). "SWE-Bench
  Pro (Public)": GPT-5.4 57.7%, GPT-5.3-Codex 56.8%, GPT-5.2-Codex 56.4%,
  GPT-5.2 55.6% ("Introducing GPT-5.4"; "Introducing GPT-5.3-Codex").
  **OpenAI never names the harness, task count or exclusions.** The only
  setup disclosed: "All evaluations in the blog were run on GPT-5.3-Codex
  with xhigh reasoning effort", and for GPT-5.4, "Benchmarks were conducted in
  a research environment, which may provide slightly different output from
  production ChatGPT". Do not write "Codex harness" or "custom scaffold" as
  if OpenAI said it. Our inference only: the chart data fits the full 731-task
  set averaged over several runs. GPT-5.2-Codex is 56.4% on OpenAI's
  undisclosed setup and 41.04% on SEAL's: a 15-point gap for one model, from
  harness, settings or both. Opus 4.6 + WarpGrep
  v2 57.5% is from Morph's own post (morphllm.com/blog/warpgrep-v2, Feb 23,
  2026): Opus 4.6 55.4% → 57.5%, Codex 5.3 56.0% → 59.1%. Morph is selling
  WarpGrep, and the post gives no harness details. A "22+ point" basic-vs-
  optimized claim from the aggregator has no source; do not use it.
- **llm-stats Verified board** [P, changed]. On 2026-09-30 it lists 116
  models, all self-reported, **0 independently verified** ("Verified0",
  "Self-reported116"). Round 1's "1 of 100" (Jun 16, 2026) can no longer be
  checked; use today's figure.
- Benchmark-literacy guide (blog, Jun 2026, updated Sep 30) [E]: scaffolding
  moves scores by 10-20 points with the model fixed. Consistent with the
  primary examples above.
- Practitioner harness deltas (LangChain, Azure SRE, statewright) are in
  `round2-harness-reference-designs.md` §8.

## 4. Cost evidence for context management [P, attribution corrected]

- The 62% figure is **not a KiloBench measurement**. Kilo's blog
  ("KiloBench – Because Your Benchmark Score Doesn't Pay the Bill", Brendan
  O'Leary, Jun 8, 2026) quotes it from elsewhere: "Audits of production teams
  show that re-sent context accounts for 62% of the total bill, with actual
  useful reasoning output comprising just 11%." Kilo links it to
  leanopstech.com (not checked). Cite it as "an industry audit cited by Kilo",
  or not at all.

## 5. Conflicts with round 1 to be aware of

- The benchmark-literacy guide gives the top SWE-bench Verified score as about
  88.6%, and the SWE-bench Pro private-set top as about 47.1% (a "41-point
  reality gap"). Round 1 recorded vendor-reported Verified tops of 95-96%
  (Opus 5, Mythos 5, Fable 5). The 88.6% matches round 1's Opus 4.8 figure,
  so the guide is probably using an older or differently filtered snapshot.
  Keep round 1's numbers, labelled vendor-reported.

## 6. Independent results for the newest models (as of Sep 30)

Tags: [P] = read on the board owner's own site or data on 2026-09-30. [S] here
means a third-party board read from Epoch AI's "external" dataset, not checked
on that board's own site.

Release dates (Epoch metadata): GPT-6 Astra Sep 3; GPT-6 Sol and Luna Sep 22;
GPT-6.1 Sol Sep 29; Fable 5 Jun 9; Sonnet 5 Jun 30; Opus 5 Jul 24; Fable 5.1
Sep 1; Opus 5.5 Sep 22; Sonnet 5.5 Sep 28; Mythos Preview Apr 7; Gemini 3.7
Flash Aug 13; Gemini 3.8 Flash Sep 2.

### 6.1 Terminal-Bench is now version 4.0 [P]

- 2.1 (May) fixed 28 broken tasks; 3.0 (Jul 30) added harder tasks; 4.0 (Aug
  28) "calibrates task resources ... and removes saturated tasks". Board data
  last updated Sep 21 (tbench.ai/leaderboard, tbench.ai/news/terminal-bench-4-0).
  Round 1's Terminal-Bench 2.1 figures are two versions old.

| Model | Harness | Effort | TB 4.0 |
|---|---|---|---|
| GPT-6 Astra | Codex | max | 58.2% ± 2.8 |
| Fable 5.1 | Claude Code | max | 57.9% ± 3.8 |
| Opus 5 | Claude Code | xhigh | 53.9% |
| Fable 5 | Claude Code | max | 44.6% |
| Grok 4.7 | Grok Build | xhigh | 37.6% |
| Gemini 3.8 Flash | mini-SWE-agent | high | 19.1% |
| Sonnet 5 | Claude Code | max | 12.4% |
| Gemini 3.7 Flash | mini-SWE-agent | high | 11.2% |

- The top two overlap within their confidence ranges. Run cost: about $3.3k
  for Astra, $6.2k for Fable 5.1.
- Not on the board: GPT-6 Sol, Luna, 6.1 Sol, Opus 5.5, Sonnet 5.5, Mythos.
- Who runs it: the board team ("our leaderboard runs"), but "The leaderboard
  experiments are supported with grants from OpenAI, Anthropic, Z.ai, SpaceX
  AI, and Laude Institute." OpenAI and Anthropic rows use each vendor's own
  harness; Gemini rows use mini-SWE-agent, which may explain part of their gap.
- **Same model, different benchmark version:** Google's 3.8 Flash model card
  cites "Terminal-bench 2.1" at 89.4% and "Terminal-bench 4.0" at 19.1%
  (summarised fetch; spot-check). A version number on a slide matters as much
  as the score.

### 6.2 Scale SEAL SWE-bench Pro [P]

No newest-generation model appears (no GPT-6, Fable, Opus 5.x, Sonnet 5.x,
Mythos or Gemini 3.5 to 3.8). The last entry looks to be about Jul 9, 2026.
Current top is in §3. The page text still says "top models score around 23%",
out of date against its own table.

### 6.3 METR time horizons [P]

- The time-horizons page has not been updated since May 8, 2026 (Time Horizon
  1.1 suite). Newest model measured: "Claude Mythos Preview (early)": 50%
  horizon about 1,045 minutes (about 17.4 hours; 95% CI 509 to 3,304
  minutes), 80% horizon about 186 minutes. METR: "Measurements above 16 hrs
  are unreliable with our current task suite".
- **No time horizon published** for any GPT-6, Fable 5.x, Opus 5.x, Sonnet
  5.x or Gemini 3.5 to 3.8 model.
- Opus 5.5 got a qualitative pre-release review only (metr.org/blog/2026-09-22-claude-opus-5-5/):
  "an incremental improvement above Fable 5.1 on our quantitative
  evaluations, rather than a discontinuous jump". On independence: "We
  drafted the initial summary, and then Anthropic had the opportunity to
  review and edit the text."
- GPT-5.6 Sol (Jun 26): METR could not get a robust number because of
  cheating: 11.3 hours if cheating counts as failure, "beyond 270hrs" if it
  counts as success. "We do not consider any of these numbers to represent a
  robust measurement". Relevant to any eval suite: graders must catch
  cheating.

### 6.4 Epoch AI [P]

- Epoch's own SWE-bench Verified runs have no newest-generation model; the
  last run started Jun 25. Best frontier entry: Opus 4.7 (max) 83.5%. Epoch
  now describes the benchmark as built from "Flawed GitHub issues".
- **MirrorCode** (Epoch's long-horizon benchmark, "co-developed with METR";
  reimplement whole programs without seeing the source): Opus 5.5 (max)
  77.4%, Fable 5.1 (high) 73.3%, Fable 5 (high) 63.9%, GPT-6 Astra (high)
  46.7% (run started Aug 30, before release). Error bars about 8 to 12
  points. No Sonnet 5.x, other GPT-6 or Gemini rows.
- [S] Third-party boards mirrored in Epoch's external data (not checked on
  the owners' sites; Cursor and Cognition sell coding agents):
  - APEX-Agents: Sonnet 5.5 75.5%, Opus 5.5 73.5%, Fable 5.1 68.6%, Gemini
    3.7 Flash 67.8%, GPT-6 Astra 64.7%, GPT-6.1 Sol 60.0%, GPT-6 Sol 54.3%,
    GPT-6 Luna 44.3%.
  - FrontierSWE V2: GPT-6 Astra 65.5% (about $1,030 per task), Opus 5.5
    62.3%, Sonnet 5.5 61.9%, Fable 5.1 56.3%, Gemini 3.8 Flash 19.6%.
  - FrontierCode (Cognition): Opus 5.5 54.6%, GPT-6 Astra 53.3%, GPT-6.1 Sol
    50.2%.
  - CursorBench (Cursor): Opus 5.5 57.8%, Sonnet 5.5 55.5%, Fable 5.1 51.8%.

### 6.5 Boards that have stopped [P]

- swebench.com: no entries after Feb 26, 2026 on any board.
- Princeton HAL: "We have paused updating HAL leaderboard with new models and
  are currently focusing on measuring reliability in AI agents." Its
  reliability dashboard stops at Opus 4.7, GPT-5.5 and Gemini 3.5 Flash.

### 6.6 Which newest models have an independent result

| Model | Independent result? |
|---|---|
| GPT-6 Astra | Yes: TB 4.0, MirrorCode |
| GPT-6 Sol, GPT-6 Luna, GPT-6.1 Sol | No |
| Fable 5, Fable 5.1 | Yes: TB 4.0, MirrorCode |
| Opus 5 | TB 4.0 only |
| Opus 5.5 | MirrorCode; METR qualitative review, no time horizon |
| Sonnet 5 | TB 4.0 only |
| Sonnet 5.5 | No |
| Mythos (Preview, early) | METR time horizon only |
| Gemini 3.7 / 3.8 Flash | TB 4.0 only, on a third-party harness |
