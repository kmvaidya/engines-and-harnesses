---
url: https://www.swebench.com/, https://openai.com/index/introducing-swe-bench-verified/, https://www.tbench.ai/leaderboard/terminal-bench/2.1, https://aider.chat/docs/leaderboards/, https://metr.org/time-horizons/, https://labs.scale.com/leaderboard/swe_bench_pro_public, https://epoch.ai/publications/what-skills-does-swe-bench-verified-evaluate
fetched: 2026-08-12
---

# Track 3 — Coding Benchmarks: State of Play (August 2026)

Research notes. Every number carries its source URL. Vendor-reported vs independently-run scores are flagged — the distinction matters more in 2026 than the scores themselves.

---

## 1. SWE-bench Verified

### What it measures
- Real GitHub issues from open-source Python repos. The agent gets the repo at the pre-fix commit + the issue text, and must produce a patch. The patch is graded by running the repo's own unit tests (fail-to-pass tests must pass, pass-to-pass tests must keep passing). https://www.swebench.com/
- **Verified** = a 500-task human-validated subset of the original SWE-bench test set, created by OpenAI + SWE-bench authors (announced Aug 2024). https://openai.com/index/introducing-swe-bench-verified/

### How the Verified subset was created
(Primary page openai.com/index/introducing-swe-bench-verified/ returned 403 to my fetcher; details below confirmed via secondary sources quoting it: https://github.com/irthomasthomas/undecidability/issues/933 , https://hyper.ai/en/datasets/33655)
- **93 professional Python developers** manually screened **1,699 randomly sampled tasks** from the SWE-bench test set; 500 survived as "Verified."
- Motivating defects found in original SWE-bench: **38.3%** of samples had underspecified problem statements; **61.1%** had unit tests that could unfairly reject valid solutions; overall **68.3%** of sampled data was removed.
- Effect: GPT-4o jumped from **16%** (original SWE-bench, best scaffold) to **33.2%** on Verified — i.e., much of the old "difficulty" was broken tasks, not hard engineering.

### Top scores as of Aug 2026 (vendor-reported, via aggregators)
I could not extract rows from the official swebench.com leaderboard (JS-rendered; the site confirms Verified/Multimodal/Multilingual/Lite/Full variants and a "Bash Only" filter but rows didn't render to my fetcher — https://www.swebench.com/). Frontier-lab numbers no longer appear there first anyway; they are self-reported in model cards and mirrored by trackers:

| Model | SWE-bench Verified | Source / notes |
|---|---|---|
| Claude Opus 5 | **96.0%** | Anthropic-reported, launch July 24, 2026 — https://www.marktechpost.com/2026/07/24/meet-the-new-claude-opus-5-frontier-class-agentic-coding-and-computer-use-at-unchanged-opus-pricing/ ; mirrored at https://benchlm.ai/benchmarks/sweVerified |
| Claude Mythos 5 | 95.5% | Anthropic-reported — https://benchlm.ai/benchmarks/sweVerified |
| Claude Fable 5 | 95.0% | Anthropic-reported, launch June 9, 2026 — https://www.morphllm.com/claude-benchmarks ; one tracker labels it "independently verified" — https://www.digitalapplied.com/blog/swe-bench-verified-june-2026-benchmark-vs-scaffolding-analysis |
| Claude Opus 4.8 | 88.6% | vendor-reported — https://benchlm.ai/benchmarks/sweVerified |
| Claude Sonnet 5 | 85.2% | vendor-reported — https://benchlm.ai/benchmarks/sweVerified |
| GPT-5.3 Codex | 85% | OpenAI-reported — https://benchlm.ai/benchmarks/sweVerified (OpenAI's own Feb 5, 2026 launch materials emphasized SWE-bench **Pro** 56.8% instead — https://codex.danielvaughan.com/2026/05/14/gpt-5-3-codex-model-deep-dive-benchmarks-cli-configuration-interactive-coding/) |
| Gemini 3.1 Pro | 80.6% | Google-reported, Feb 19, 2026 — https://medium.com/@leucopsis/gemini-3-1-pro-review-1403a8aa1a96 (Gemini 3 Pro was 76.2%, up from 59.6% for 2.5 Pro — same source) |
| Claude Opus 4.5 / 4.6 | 80.9% / 80.8% | vendor-reported — https://benchlm.ai/benchmarks/sweVerified |
| Open-weight cluster (DeepSeek V4 Pro, MiniMax M3, Qwen3.7 Max, Kimi K2.6) | 80.2–80.6% | vendor-reported — https://benchlm.ai/benchmarks/sweVerified |

- Trackers sourced from llm-stats show a slightly different top (Claude Mythos Preview 93.9%) — https://www.codesota.com/benchmark/swe-bench-verified-agentic — illustrating that "the" leaderboard no longer exists; every aggregator mixes vendor numbers differently.
- Key caveat: of 100 models listed on llm-stats (June 16, 2026 snapshot), **99 scores were vendor-submitted; only 1 carried an independent verification badge** — https://www.digitalapplied.com/blog/swe-bench-verified-june-2026-benchmark-vs-scaffolding-analysis
- **OpenAI's Frontier Evals team publicly stopped reporting SWE-bench Verified in early 2026** (saturation + contamination; see critiques file) — https://www.latent.space/p/swe-bench-dead

### THE SCAFFOLD MATTERS AS MUCH AS THE MODEL — concrete deltas
SWE-bench scores are properties of a **system** (model + agent harness/scaffold + prompts + tools + retry budget), not of a model. Evidence:

| Same model, different scaffold | Score delta | Source |
|---|---|---|
| GPT-4o, different scaffolds on Verified | 23% → 33.2% (**+10.2 pp**) | https://epoch.ai/publications/what-skills-does-swe-bench-verified-evaluate |
| Claude 3.7, generic vs custom scaffold | 62.3% → 70.2% (**+7.9 pp**) | https://epoch.ai/publications/what-skills-does-swe-bench-verified-evaluate |
| DeepSeek R1-0528, scaffold switch | 33% → 57.6% (**+24.6 pp**) | https://epoch.ai/publications/what-skills-does-swe-bench-verified-evaluate |
| Claude Opus 4.5, three different harnesses (SWE-bench Pro) | 50.2%–55.4% (**5.2 pp spread**, model identical) | https://www.digitalapplied.com/blog/swe-bench-verified-june-2026-benchmark-vs-scaffolding-analysis |
| Anthropic vendor scaffold vs Scale's standardized SEAL harness (SWE-bench Pro) | Opus 4.8 vendor 69.2% vs best Claude on SEAL board 51.9% (**~17.3 pp vendor advantage**) | https://www.digitalapplied.com/blog/swe-bench-verified-june-2026-benchmark-vs-scaffolding-analysis |
| Terminal-Bench 2.1, same model different agent (see §2) | Fable 5: Claude Code 83.8% vs Terminus 2 80.4%; Gemini 3 Pro: Terminus 2 73.9% vs Gemini CLI 65.8% | https://www.tbench.ai/leaderboard/terminal-bench/2.1 |

- Epoch AI's summary judgment: "performance on SWE-bench Verified reflects the sophistication of the scaffold as much as the capability of the underlying model" — https://epoch.ai/publications/what-skills-does-swe-bench-verified-evaluate
- Anthropic said this themselves in Oct 2024 when Claude 3.5 Sonnet took SOTA at **49%** with a deliberately simple scaffold (just a bash tool + string-replace edit tool): "the performance of an agent on SWE-bench can vary significantly based on this scaffolding, even when using the same underlying AI model" — https://www.anthropic.com/engineering/swe-bench-sonnet
- Counter-trend: **mini-swe-agent**, a ~100-line Python scaffold with bash as its only tool, scores **>74% on Verified** (was 65% at launch, July 2025) — as models improve, minimal scaffolds close the gap with bespoke ones — https://github.com/SWE-agent/mini-swe-agent , https://news.ycombinator.com/item?id=44682897
- Independent re-runs: Epoch AI re-benchmarks models in its own standardized harness (simple action loop; bash + text_editor + apply_patch tools, plus Claude Code/Codex third-party scaffolds via Inspect-SWE); methodology upgraded to v2.0 in Feb 2026 — https://epoch.ai/benchmarks/swe-bench-verified . Epoch's numbers routinely land below vendor-reported ones (harness, retry and token-budget differences) — https://www.futureagi.com/blog/coding-agent-harness-benchmark/ (see also https://futureagi.com/blog/coding-agent-harness-benchmark/)

---

## 2. Terminal-Bench

### What it measures
- Agent tasks executed in a sandboxed terminal (Docker) — package management, builds, git, server config, shell scripting, ML/data/security/sysadmin tasks — verified by tests over the resulting environment state. Open project led by **Stanford University + Laude Institute** — https://github.com/laude-institute/terminal-bench , https://www.tbench.ai/
- Runs on **Harbor**, the project's execution harness connecting an agent to the terminal sandbox (parallelized evals; also used for RL environments). Harbor + Terminal-Bench 2.0 released ~Nov 5, 2025 — https://snorkel.ai/blog/terminal-bench-2-0-raising-the-bar-for-ai-agent-evaluation/
- Current version: **2.0 and 2.1 both live; 2.1 is the primary leaderboard** (released May 6, 2026; fixed 28 tasks, added continuous validation). Scores NOT comparable across versions — https://www.tbench.ai/news/terminal-bench-2-1 , https://www.tbench.ai/leaderboard

### Terminal-Bench 2.1 official leaderboard (fetched 2026-08-12)
Source: https://www.tbench.ai/leaderboard/terminal-bench/2.1

| # | Agent (scaffold) | Model | Score | Date |
|---|---|---|---|---|
| 1 | Claude Code | Claude Fable 5 | 83.8% | Jun 7, 2026 |
| 2 | Codex | GPT-5.5 | 83.1% | May 1, 2026 |
| 3 | Terminus 2 | Claude Fable 5 | 80.4% | Jun 5, 2026 |
| 4 | Cursor CLI | Grok 4.5 | 79.3% | Jul 9, 2026 |
| 5 | Claude Code | Claude Opus 4.8 | 78.9% | Jul 9, 2026 |
| 6 | Codex | GPT-5.6 Terra | 78.4% | Jul 11, 2026 |
| 7 | Terminus 2 | GPT-5.5 | 78.0% | May 1, 2026 |
| 8 | mini-SWE-agent | Muse Spark 1.1 | 76.2% | Jul 9, 2026 |
| 9 | Codex | GPT-5.6 Luna | 75.7% | Jul 11, 2026 |
| 10 | Claude Code | Claude Sonnet 5 | 74.6% | Jul 9, 2026 |
| 11 | Terminus 2 | Gemini 3 Pro | 73.9% | May 1, 2026 |

- Note the built-in scaffold experiment: Terminus 2 is the benchmark's reference agent, so rows 1 vs 3 (Fable 5: 83.8 vs 80.4) and 11 vs Gemini CLI (Gemini 3 Pro: 73.9 vs 65.8) are same-model, different-harness deltas — https://www.tbench.ai/leaderboard/terminal-bench/2.1
- Vendor-reported numbers not (yet) on the official board run higher: Claude Mythos 5 **88.0%**, Kimi K3 + KimiCode **88.3%** (both TB 2.1, vendor model cards) — https://codingfleet.com/blog/terminal-bench-leaderboard-2026/ . One aggregator (pricepertoken) lists a "top" of GPT-5.6 Sol 65.9% under a different methodology — tracker fragmentation is real; treat only tbench.ai as canonical — https://pricepertoken.com/leaderboards/benchmark/terminalbench
- On TB 2.0 (older, easier): GPT-5.3-Codex reported 77.3% vs 64.0% for GPT-5.2-Codex — https://codex.danielvaughan.com/2026/05/14/gpt-5-3-codex-model-deep-dive-benchmarks-cli-configuration-interactive-coding/

---

## 3. Aider Polyglot benchmark

### What it measures
- **225 of the hardest Exercism exercises** across C++, Go, Java, JavaScript, Python, Rust. Tests whether a model can follow instructions and emit correct code **in aider's structured edit format**, inside aider's real edit loop; one retry with failing unit-test output. Measures instruction-following + editing discipline, not repo-scale engineering — https://aider.chat/docs/leaderboards/

### Current leaderboard state (fetched 2026-08-12)
Source: https://aider.chat/docs/leaderboards/

| # | Model | % correct | % correct edit format | Cost |
|---|---|---|---|---|
| 1 | gpt-5 (high) | 88.0% | 91.6% | $29.08 |
| 2 | gpt-5 (medium) | 86.7% | 88.4% | $17.69 |
| 3 | o3-pro (high) | 84.9% | 97.8% | $146.32 |
| 4 | gemini-2.5-pro-preview-06-05 (32k think) | 83.1% | 99.6% | $49.88 |
| 5 | gpt-5 (low) | 81.3% | 86.7% | $10.37 |

- **Important caveat: this leaderboard is effectively stale.** Top entries are all 2025-era models (gpt-5, o3, gemini-2.5); none of the 2026 frontier (Opus 5, Fable 5, GPT-5.3+, Gemini 3.x) appear. Mirrors confirm gpt-5 (high) 88.0% is still the tracked top as of mid-2026 — https://llm-stats.com/benchmarks/aider-polyglot . Useful historically; no longer a live frontier signal.

---

## 4. Other benchmarks that matter for coding-model choice

### LiveCodeBench (contamination-aware, rolling)
- Competitive-programming problems continuously scraped from LeetCode/AtCoder/Codeforces, **tagged with release date** so you can score models only on problems published after their training cutoff — the core contamination defense — https://livecodebench.github.io/ , https://arxiv.org/abs/2403.07974
- Current top (tracker, Aug 12, 2026): Gemini 3 Pro Preview **91.7%**, Gemini 3 Flash Preview 90.8%, DeepSeek V3.2 Speciale 89.6%; ~194 models evaluated — https://pricepertoken.com/leaderboards/benchmark/livecodebench . Open-weight models (DeepSeek, Qwen coder line) frequently lead the rolling-cutoff split — https://agileleadershipdayindia.org/blogs/ai-coding-benchmarks-decoded/livecodebench-contamination-resistant-leaderboard.html

### METR long-task time horizons (measurement paradigm, not a leaderboard)
- METR measures the **length of task (in human-expert time) an agent completes with 50% success**, instead of a static pass rate. Landmark March 2025 result: this 50% time horizon has doubled roughly every **7 months since 2019** — https://metr.org/blog/2025-03-19-measuring-ai-ability-to-complete-long-tasks/ , https://arxiv.org/abs/2503.14499
- **Time Horizon 1.1** (Jan 29, 2026): task suite grown 170 → 228 tasks, 8h+ tasks doubled (14 → 31), infra moved to Inspect. Doubling times: full trend **196.5 days (~7 months)**; since-2023 **130.8 days**; since-2024 **88.6 days** — progress is accelerating — https://metr.org/blog/2026-1-29-time-horizon-1-1/
- Frontier 50% horizons at TH1.1 release: Claude Opus 4.5 ≈ **320 min (~5.3 h)** [CI 170–729], GPT-5 ≈ 214 min (~3.6 h), o3 ≈ 121 min (~2 h), Claude Opus 4 ≈ 101 min — https://metr.org/blog/2026-1-29-time-horizon-1-1/ (unit note: my page extraction rendered these as "hours," but METR's own paper describes o3's horizon as "nearly two hours," confirming minutes; treat with that caveat). Secondary trackers report Claude Opus 4.6's 50% horizon at roughly **12 hours** in later 2026 measurements — I could not verify this exact figure on metr.org directly; METR itself warns "measurements above 16 hrs are unreliable with our current task suite" — https://metr.org/time-horizons/ (page last updated May 8, 2026; raw data: /assets/benchmark_results_1_1.yaml)

### SWE-bench Pro (the designated successor)
- Scale AI, Sept 2025: **1,865 tasks across 41 professional repos** — public set 731 (GPL repos), private/commercial set 276 (proprietary startup codebases), held-out 858. Contamination defense: copyleft licensing + genuinely private code; tasks are longer (1–4+ h) and multi-file — https://labs.scale.com/leaderboard/swe_bench_pro_public
- At launch, top models scored ~23% (vs 70%+ on Verified at the time) — same source. **OpenAI's Frontier Evals team now endorses Pro as the successor to Verified** — https://www.latent.space/p/swe-bench-dead
- Scale SEAL standardized public leaderboard (fetched 2026-08-12): Muse Spark 1.1 **61.5±3.1**, gpt-5.4 (xHigh) 59.1, Muse Spark 55.0, claude-opus-4-6 (thinking) 51.9, gemini-3.1-pro (thinking) 46.1, claude-opus-4-5 45.9 — https://labs.scale.com/leaderboard/swe_bench_pro_public
- Vendor-reported Pro numbers are much higher than SEAL-standardized ones: Claude Fable 5 80.0%, Claude Opus 5 79.2% (Anthropic materials — https://www.marktechpost.com/2026/07/24/meet-the-new-claude-opus-5-frontier-class-agentic-coding-and-computer-use-at-unchanged-opus-pricing/), GPT-5.3-Codex 56.8% (OpenAI — https://codex.danielvaughan.com/2026/05/14/gpt-5-3-codex-model-deep-dive-benchmarks-cli-configuration-interactive-coding/). The vendor-vs-standardized gap is the scaffold story again.

### Multi-SWE-bench (multilingual)
- ByteDance; **1,632 human-validated issues across 7 languages** (Java, TS, JS, Go, Rust, C, C++); NeurIPS 2025 D&B; mini (400 instances / 8 languages) and flash (300 instances) variants — https://github.com/multi-swe-bench/multi-swe-bench , https://arxiv.org/abs/2504.02605

### SWE-bench Live (auto-refreshing)
- Microsoft; automatically updated task set from issues created **since 2024** — currently **1,890 tasks from 223 repos**; NeurIPS 2025 D&B. 2026 expansions: MultiLang split (743 tasks, 6 languages, 381 repos, as of May 16, 2026) with leaderboard Jan 10, 2026; **Windows split** (61 tasks, 44 repos) with leaderboard Aug 3, 2026 — https://github.com/microsoft/SWE-bench-Live , https://swe-bench-live.github.io/

### LMArena WebDev Arena (human preference)
- Live pairwise arena: two anonymous models each build a web app from the same prompt in a sandbox; humans vote. As of May 24, 2026: top model **claude-opus-4-7-thinking, Elo 1567**, after 288,203 votes over 77 models; 5 of the top 10 slots were Claude variants — https://modelgauntlet.com/leaderboard/web-development/ (arena itself: https://web.lmarena.ai/). Complements execution benchmarks with taste/UX signal; vulnerable to style bias.

---

## One-slide takeaway
- Verified is saturated (top cluster 95–96%, vendor-reported) and the ecosystem is migrating to SWE-bench Pro, Terminal-Bench 2.1, SWE-bench Live, and METR-style time horizons.
- Any SWE-bench number without its harness named is under-specified: same-model scaffold swings of +5 to +25 pp are documented (Epoch AI), and vendor harnesses beat standardized ones by ~10–17 pp (Scale SEAL vs model cards).
