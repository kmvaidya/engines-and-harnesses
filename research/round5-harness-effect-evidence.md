---
url: https://arxiv.org/abs/2605.23950, https://arxiv.org/html/2605.23950v1, https://arxiv.org/abs/2608.26218, https://arxiv.org/html/2608.26218v1, https://github.com/sydches/yuj, https://arxiv.org/abs/2603.28052, https://arxiv.org/html/2603.28052v1, https://arxiv.org/abs/2604.25850, https://arxiv.org/abs/2609.08149, https://arxiv.org/html/2609.08149, https://arxiv.org/abs/2610.24206, https://arxiv.org/html/2610.24206v1, https://arxiv.org/abs/2609.00006, https://arxiv.org/html/2609.00006, https://arxiv.org/abs/2604.03515, https://arxiv.org/html/2604.03515, https://arxiv.org/abs/2607.24882, https://arxiv.org/html/2607.24882, https://www.morphllm.com/swe-bench-pro, http://web.archive.org/web/20260403125229/https://www.morphllm.com/swe-bench-pro, http://web.archive.org/web/20260701120601/https://www.morphllm.com/swe-bench-pro, https://www.augmentcode.com/blog/auggie-tops-swe-bench-pro, https://www.tbench.ai/leaderboard/terminal-bench/4.0, https://ofhuhcpkvzjlejydnvyd.supabase.co/functions/v1/leaderboard-read, https://www.tbench.ai/news/leaderboard-integrity-update, https://www.vals.ai/benchmarks/terminal-bench-4, https://www.vals.ai/benchmarks/terminal-bench-2-1, https://www.vals.ai/benchmarks/terminal-bench-2, https://factory.com/news/frontier-harness, https://github.blog/ai-and-ml/github-copilot/evaluating-performance-and-efficiency-of-the-github-copilot-agentic-harness-across-models-and-tasks/, https://agentmarketcap.ai/blog/2026/10/06/forgecode-terminal-bench-answer-key-injection-benchmark-fraud, https://aiweekly.co/alerts/openai-drops-swe-bench-verified-backs-pro-after-flaw-audit
fetched: 2026-11-04
---

# Does the harness change outcomes when the model is held constant?

Round 5 gap-filling file. Companion to `track3-benchmarks.md` ("THE SCAFFOLD
MATTERS"), `track3-benchmark-critiques.md`, `round2-evals-and-benchmarks.md`
§1, §3 and §6, `round5-platforms-research.md` §4.8 and
`round5-copilot-architecture.md` §7.

**Tags.** [P] confirmed on the primary page (paper full text, vendor page,
leaderboard data). [P\*] primary source, but the number is quoted by another
primary source and not checked at its origin. [S] secondary only. [E]
extracted, not cross-checked. [R] refuted or misquoted (recorded so nobody
reuses it). [O] our analysis. "Vendor claim" marks numbers a company reports
about its own product.

## Short version

- **The headline 45.9% vs 55.4% figure is wrong.** arXiv 2605.23950 says
  Opus 4.5 scores 45.9% on SWE-bench Pro under Scale's SEAL scaffold and
  55.4% under Claude Code. The 55.4% comes from a Morph aggregator page. The
  primary source for the Claude Code row (Augment's own run) says 49.75%.
  The real gap is 3.9 points, or 5.9 points to the best product harness
  (Auggie, 51.80%) [R]. Round 2 had already caught the same 55.4% error in
  our round 1 files.
- **Controlled studies do show large same-model effects, but only where the
  harness fixes a binding problem.** In 2608.26218 one harness change took
  Qwen3.6 on SWE-bench Verified from 43 to 72 solved tasks under a 20k-token
  window, and to no difference (102 vs 101) at 262k tokens [P]. In
  2605.23950's own 3x3 grid, harness changes moved scores 8.5 to 13 points
  and model changes 2.5 to 5 points, but on 100 tasks, two runs, and against
  a deliberately weak baseline harness [P].
- **The newest independent evidence points the other way for strong
  models.** Scale's SWE-Bench Pro V2 (Oct 16, 2026) ran three open-weight
  models in mini-swe-agent, Pi and OpenCode: "the task explains 32% of the
  variance in solved-or-failed, the model 2.7% and the scaffold 0.3%" [P].
  On Terminal-Bench 4.0, frontier models score within about 3 points in
  their vendor harness (tbench.ai) and in bash-only mini-SWE-agent (vals.ai)
  for 10 of 16 model pairs we could match [P data, O comparison].
- **Terminal-Bench 4.0 has no same-model, different-agent rows.** All 35
  rows on the official board use one agent per model (Claude Code, Codex,
  mini-SWE-agent, Grok Build, Muse Code) [P]. Same-model rows exist only on
  the older 2.0 and 2.1 boards. On 2.0 the spread for one model reaches
  18.4 points (Opus 4.6), but most top rows are unverified third-party
  submissions, and the board's own integrity post records reward hacking by
  one of them [P].
- **Vendor head-to-heads disagree with the official board.** Factory's
  Terminal-Bench 4 run puts Claude Code with Opus 5.5 at 57.6%; the official
  board has the same pair at 64.8% ± 3.1 (different effort setting) [P,
  vendor claim]. GitHub's parity study reports "effective parity" with
  Claude Code and Codex CLI, with "best scored run" reporting on small
  benchmarks [P, vendor claim].
- **What a presenter can honestly say:** the harness is part of what gets
  measured, so a score without the harness named is incomplete; harness
  changes can move a weak or constrained setup a lot; for current frontier
  models on well-graded tasks, the measured gap between a good product
  harness and a minimal one is small, a few points, and often inside the
  noise. See §9.

---

## 1. arXiv 2605.23950, "Stop Comparing LLM Agents Without Disclosing the Harness"

**Paper.** Yunbei Zhang, Janet Wang, Yingqiang Ge, Weijie Xu, Jihun Hamm,
Chandan K. Reddy (Tulane, Rutgers, independent, Virginia Tech). Submitted May
7, 2026, v1 only. Position paper. [P] https://arxiv.org/abs/2605.23950, full
text read at https://arxiv.org/html/2605.23950v1.

**Thesis, verbatim [P].** "the agent execution harness ... is often a
stronger determinant of agent performance than the model it wraps." They
name it the Binding Constraint Thesis and restrict it to "long-horizon tasks
evaluated across models with comparable frontier capability". Closing line:
"Until harness specifications are disclosed, leaderboard comparisons for
long-horizon agents should be treated as incomplete and potentially
misleading."

### 1.1 The 45.9% vs 55.4% figure: does it hold?

- [P] §2.1: "Under the standardized SEAL scaffold on SWE-bench Pro, Claude
  Opus 4.5 reaches 45.9%, while under Claude Code the same model reaches
  55.4%." Table 1 row: "SEAL → Claude Code ... +9.5pp (45.9% → 55.4%)".
  Source given: reference [25], Morph, "SWE-Bench Pro Leaderboard (2026): Why
  46% Beats 81%".
- [P] The Morph page (live URL blocked by a Vercel checkpoint and then HTTP
  429; read through Wayback snapshot of Apr 3, 2026, before the paper's
  submission) has an "Agent Systems Leaderboard (Custom Scaffolding)" with
  "Auggie | Opus 4.5 | 51.8% | Augment Code", "Cursor | Opus 4.5 | 50.2% |
  Cursor", "Claude Code | Opus 4.5 | 55.4% | Anthropic", and "Scores are
  self-reported by each team."
- [P] The Auggie and Cursor numbers on Morph match Augment's post, which is
  where all three product rows were run: "Auggie (Claude Opus 4.5) 51.80%,
  Cursor 50.21%, Claude Code 49.75%, SWE-Agent 45.89%", 731 problems, all
  three products run by Augment, Feb 4, 2026, updated Jun 18. The SWE-Agent
  row is not Augment's run: "SWE-Agent baseline is from Scale AI leaderboard
  (Jan 2026)"; the page does not use the word SEAL. The Augment page does
  not contain 55.4. https://www.augmentcode.com/blog/auggie-tops-swe-bench-pro
- [P, from round 2] 55.4% is Opus **4.6**'s baseline in Morph's WarpGrep v2
  post (Opus 4.6 55.4% → 57.5% with WarpGrep). Anthropic's Opus 4.5 System
  Card gives 52.0% on SWE-bench Pro under Anthropic's own setup.
  (`round2-evals-and-benchmarks.md` §3.)
- [P] In the Wayback capture of Jul 1, 2026 (page marked "Updated June 28,
  2026") the agent-systems table is gone and
  55.4% now appears as DeepSeek-V4-Pro-Max's vendor score, so the error can
  no longer be seen on the live page.
- **Verdict [R].** "Claude Code + Opus 4.5 = 55.4% on SWE-bench Pro" is an
  aggregator error that the paper propagated. Corrected same-model figures on
  the 731-task public set: SEAL/SWE-Agent 45.89%, Claude Code 49.75%, Cursor
  50.21%, Auggie 51.80% (Augment-run, vendor claim for Auggie). SEAL to
  Claude Code is +3.9 points, not +9.5. The three product harnesses span 2.05
  points.
- [O] Knock-on effect on §4.1 of the paper. It argues the within-model
  harness range (9.5 points) "exceeds the within-harness model range by
  roughly twofold" (4.9 points across six models on SEAL). With the corrected
  figure the within-model range is 5.9 points (45.89 to 51.80), about 1.2
  times the 4.9-point model range. Also, the SEAL model range of 41.0% to
  45.9% was Morph's March snapshot; SEAL's own board later had Muse Spark 1.1
  at 61.50 (round 2 §3), so the "4.9 points" was already stale.

### 1.2 The other observational evidence in the paper

All [P\*]: quoted in the paper's §2.1, §4.1 and Table 1, not checked at
origin unless noted.

| Claim in paper | Numbers | Paper's source | Our status |
|---|---|---|---|
| Grok 4, SWE-agent → xAI scaffold, SWE-bench Verified | 58.6% → 72–75% (+14–16) | Vals AI, Anthropic [37, 32] | [P\*] |
| Terminal-Bench 2.0, fixed model, prompt + middleware + verification | 52.8% → 66.5% (+13.7) | LangChain (Trivedy) [36] | [P] in `round2-harness-reference-designs.md` §8 (gpt-5.2-codex, vendor-run) |
| Terminal-Bench 2, GPT-5.4 (high), AHE harness evolution | 69.7% → 77.0% (+7.3) | AHE, arXiv 2604.25850 [17] | [P] abstract: "ten AHE iterations lift pass@1 on Terminal-Bench 2 from 69.7% to 77.0%, surpassing the human-designed harness Codex-CLI (71.9%)"; the model name GPT-5.4 is [P\*] (not in the abstract) |
| HAL, SWE-bench Verified Mini, SWE-Agent vs HAL Generalist | Sonnet 4.5 68% vs 34%; GPT-5 Medium 46% vs 12%; o4-mini nearly 48 points | HAL, arXiv 2510.11977 [14] | [P\*] |
| Epoch, scaffold-only variation on SWE-bench Verified | up to 11 points (GPT-5), 15 (Kimi K2 Thinking) | Epoch "Why benchmarking is hard" [4] | [P\*] |
| Vercel, 15 tools → 2 tools | 80% → 100% | Qu, "We removed 80% of our agent's tools" [29] | [P\*], single vendor anecdote |
| WarpGrep subagent on SWE-bench Pro | +2.1 to 2.2 points per model | Morph [25] | [P\*], vendor claim (Morph sells WarpGrep) |
| SWE-bench Pro, Opus 4.5, SEAL → Claude Code | 45.9% → 55.4% | Morph [25] | **[R]**, see §1.1 |

### 1.3 The controlled factorial (the paper's own experiment)

- [P] Setup: GPT-5.4, Kimi K2.6, GLM-5.1, picked because they were "tightly
  clustered on the LLM Stats coding leaderboard". Appendix B: "on the April
  23, 2026 snapshot, Kimi K2.6, GLM-5.1, and GPT-5.4 had coding scores of
  45.4, 45.3, and 44.6, respectively." [R, fixed in verification pass: the
  earlier wording listed the scores in GPT-5.4, Kimi, GLM order, which
  implied GPT-5.4 had 45.4; it had 44.6.] 100-task difficulty-stratified subset
  of SWE-bench Verified (seed 42), two runs per cell, 50-step budget, 120 s
  per step, max output 4,096 tokens.
- [P] Harnesses: H1 "Minimal" (no compression, verbose tool schema, no retry,
  raw tool errors, 200k append-only context, empty patches allowed); H2
  "Improved" (32k compressed context, BM25 retrieval over older steps,
  minimal tool schema, structured errors, retries); H3 "Full" (H2 plus
  per-step self-check, drift checks, anomaly detection, checkpoint
  rollback, full output validation).
- [P] Table 2, mean pass@1:

| Model | H1 | H2 | H3 |
|---|---|---|---|
| GLM-5.1 | 52.5 | 56.5 | 65.5 |
| GPT-5.4 | 55.0 | 58.5 | 63.5 |
| Kimi K2.6 | 52.0 | 59.0 | 60.5 |

- [P] "Changing the harness moves GLM-5.1 by 13.0 percentage points and
  GPT-5.4 and Kimi K2.6 by 8.5 points each. Changing the model within a fixed
  harness moves scores by only 3.0, 2.5, and 5.0 points for H1, H2, H3."
  Aggregate HV/MV ratio 7.80x (run-level 8.72x and 6.76x). "We do not claim
  that the 7.80× ratio is universal."
- [P] Cost: H2 was the cheapest harness for GPT-5.4 ($22.19 vs $34.19 for H1)
  and roughly halved tokens (9.7M vs 18.9M). Total experiment $215.79.
- [P] Mechanism (Appendix E): H1→H2 "reduces control noise rather than
  increasing model knowledge"; H2→H3 gains "come primarily from closing the
  verification and recovery loop".
- [O] Caveats a presenter needs:
  1. 100 tasks and two runs. The binomial standard error at 55% on 100 tasks
     is about 5 points, so the 2.5 to 5 point model differences are inside
     noise and the "6 of 9 ranking reversals" are what noise between
     near-tied models would produce. The 8.5 to 13 point harness effects are
     larger than that, but not by a wide margin.
  2. The models were chosen because they score alike, which keeps the
     model variance small by design. The thesis is scoped to that case, so
     this is not a flaw, but it means the 7.8x ratio says nothing about
     comparing a frontier model with a weaker one.
  3. H1 is a strawman next to any product harness (no retry, raw errors,
     empty patches accepted). The study measures "bad harness vs decent
     harness", not "Claude Code vs Copilot".
  4. It is a position paper by authors arguing the thesis, single venue,
     not peer reviewed as far as arXiv shows.
- [P] Useful for a bank audience: the paper's seven-layer "Harness Card"
  disclosure list (Execution, Tool, Context, Scheduling, Observability,
  Verification, Governance; Table 3). Governance asks for "Permission model,
  allowlist/denylist rules, side-effect boundaries, secret handling, and
  human approval points."

## 2. arXiv 2608.26218, "Same Model, Different Harness: Different Coding-Agent Results"

**Paper.** Sydney Lewis, single author, submitted Aug 26, 2026, v1 only.
Harness: Yuj, built by the author (https://github.com/sydches/yuj). [P] Full
text read at https://arxiv.org/html/2608.26218v1.

- [P] Design: one harness, two configurations. Control shows the full
  chronological transcript and stops when it fills the window. Treatment
  keeps the same record but "mechanically shortens older tool results as the
  context fills and responds to repeated or stalled work", plus command
  safeguards. No model summaries. Paired by task: same weights, tasks,
  window, tool interface, evaluator. One greedy trajectory per task per arm.
- [P] Control check: untreated Yuj and mini-SWE-agent v2.2.8 on all 500
  Verified tasks with GPT-5.5 "agreed on 87.6% of task outcomes (Cohen's
  kappa = 0.66)".
- [P] Primary model: Qwen3.6-35B-A3B, four-bit Q4_K_XL, served locally with
  llama-server. Windows deliberately shrunk to create "context pressure".
- [P] Table 2 (pressure comparisons; the McNemar column is ours, taken from
  the paper's Table 7 and §3.5, since Table 2 itself has no McNemar test):

| Benchmark (window) | n | Mean per-task F2PF C → T | Solved C → T | McNemar |
|---|---|---|---|---|
| SWE-bench Verified (20,480) | 169 | 28% → 49% | 43 → 72 | 34:5, p<0.0001 |
| SWE-bench Pro (49,152) | 316 | 15% → 33% | 31 → 72 | 47:6, p<0.0001 |
| FeatureBench (47,104) | 183 | 11% → 20% | 2 → 3 | 1:0, p=1 |

- [P] With context effectively unconstrained (262,144 tokens) the effect
  vanishes on two of three benchmarks: Verified 102 vs 101 solved, F2PF
  difference "-0.3 percentage points (95% interval [-4.5, +3.9])"; Pro 101
  vs 99. FeatureBench F2PF still rises, 23.9% → 30.7%, with 5 vs 5 solved.
- [P] Middle window (43,008) on Verified: 76 → 87 solved, p=0.0614.
- [P] Same frozen treatment on three more open-weight models (Verified, 20k
  window): Devstral 22 → 53 solved; Nemotron 16 → 25; Qwen3.8 32 → 54.
- [P] Treatment used more compute: Verified pressure cohort 3,280 vs 6,517
  model turns, 1.3 vs 4.6 solver hours. "differences in realized model work
  after control reached its context limit are part of that effect rather
  than a compute-matched efficiency estimate."
- [P] Scope statement: "four locally served open-weight checkpoints ...
  higher-precision weights and hosted frontier models lie outside the tested
  set." The operating point was "not select[ed] through a task-disjoint
  hyperparameter study".
- [P] Abstract (not the Conclusion section, which words it differently),
  verbatim: "Because changing the harness changed what
  unchanged model weights could accomplish, coding-agent evaluations should
  treat the model and harness together as the tested solver."
- [O] Reading: this is the cleanest same-model, one-variable evidence in the
  set, and it shows the harness matters a great deal when it removes a
  binding constraint (here, a small context window) and hardly at all when
  the constraint is absent. Product harnesses on 200k to 1M-token frontier
  models are closer to the 262k row than the 20k row, except on very long
  tasks.

## 3. arXiv 2603.28052, Meta-Harness

**Paper.** Yoonho Lee, Roshen Nair, Qizheng Zhang (Stanford), Kangwook Lee
(KRAFTON), Omar Khattab (MIT), Chelsea Finn (Stanford). Submitted Mar 30,
2026, v1. [P] https://arxiv.org/html/2603.28052v1

- [P] Abstract: "The performance of large language model (LLM) systems
  depends not only on model weights, but also on their harness: the code
  that determines what information to store, retrieve, and present to the
  model." Meta-Harness is an outer loop in which a coding agent (Claude Code
  with Opus 4.6) reads prior candidates' code, scores and traces from a
  filesystem and proposes new harness code.
- [P] Results: text classification "improves over a state-of-the-art context
  management system by 7.7 points while using 4× fewer context tokens"; one
  discovered math-retrieval harness "improves accuracy on 200 IMO-level
  problems by 4.7 points on average across five held-out models"; on
  TerminalBench-2 "discovered harnesses surpass the best hand-engineered
  baselines".
- [P] Table 7, TerminalBench-2 (89 tasks), scores for other agents "from the
  official leaderboard" (as of early 2026):
  - Opus 4.6: Claude Code 58.0, Terminus 2 62.9, Mux 66.5, Droid 69.9,
    TongAgents 71.9, MAYA-V2 72.1, Terminus-KIRA 74.7, Capy 75.3, ForgeCode
    81.8, **Meta-Harness 76.4**.
  - Haiku 4.5: OpenHands 13.9, Claude Code 27.5, Terminus 2 28.3,
    Mini-SWE-Agent 29.8, Terminus-KIRA 33.7, Goose 35.5, **Meta-Harness
    37.6**.
- [P] On ForgeCode: "we were unable to reproduce their reported result from
  the publicly available code alone, suggesting their leaderboard scores
  depend on components beyond the published repository."
- [P] What the search found: environment bootstrapping, a shell snapshot of
  the sandbox injected before the first turn, "roughly 80 lines on top of
  Terminus-KIRA". It "gains on 7 of 89 tasks" over Terminus-KIRA.
- [P] Caveat stated by the authors: "we perform search and final evaluation
  on the same 89-task benchmark", defended as "standard practice" and
  checked by manual and regex audits for task-string leakage.
- [P] The paper says Meta-Harness is "ranking #2 among all Opus 4.6 agents"
  and compares itself only with "the hand-engineered Terminus-KIRA (74.7%)",
  the harness it was built on. It reports no confidence intervals for the
  TerminalBench-2 numbers.
- [R, corrected in verification pass] Earlier text called Terminus-KIRA
  (74.7) "the strongest hand-built harness". The paper's own Table 7 lists
  Capy at 75.3, above Terminus-KIRA (ForgeCode's 81.8 excluded as
  unreproducible). The paper never mentions Capy in its text.
- [O] So the Opus 4.6 gain is 1.7 points over the base harness it extends
  (74.7) and 1.1 points over the best reproducible hand-built row (Capy
  75.3). Both are inside the leaderboard's roughly ±2.4 to 2.6 point 95%
  intervals (interval width is from the leaderboard, not the paper), and
  they were measured on the search set. The striking number in this paper
  is the leaderboard spread it reproduces (Opus 4.6 from 58.0 in Claude Code
  to 75.3 in Capy, or 81.8 counting ForgeCode), not its own increment.

## 4. Terminal-Bench leaderboards: same model, different agent

### 4.1 Terminal-Bench 4.0 (official board, tbench.ai)

Verification note (2026-11-04): the official-board numbers in §4.1, §4.3
and §4.4 could not be re-fetched in the verification pass and are [E] until
rechecked; only the Opus 5.5 64.8% ± 3.1 row was corroborated, through a
third-party mirror. vals.ai numbers were re-confirmed.

- [P] Data read from the board's JSON (the page server-renders 4.0; other
  versions load through the Harbor endpoint
  `ofhuhcpkvzjlejydnvyd.supabase.co/functions/v1/leaderboard-read`).
  Leaderboard "updated_at" Oct 23, 2026; 35 rows; each row 330 trials (66
  tasks).
- [P] **There are no same-model rows with different agents on 4.0.** Every
  model appears with one agent: Anthropic models, GLM-5.3, GLM-5.3-Flash and
  Qwen3.8-Max-0902 with Claude Code; OpenAI models with Codex; Gemini 3.7 and
  3.8 Flash with mini-SWE-agent; Grok with Grok Build; Muse Spark 1.3 with
  Muse Code. Different rows for one model differ only in reasoning effort.
  The same is true of the 3.0 board (12 rows, updated Sep 3).
- [P] Top rows: Opus 5.5 / Claude Code / max 64.8% ± 3.1; Sonnet 5.5 /
  Claude Code / max 61.8%; GPT-6 Astra / Codex / max 58.2%; GPT-6.1 Sol /
  Codex / max 58.2%; Fable 5.1 / Claude Code / max 57.9%.
- [P] Effort moves scores as much as harness claims do: Opus 5 in Claude
  Code ranges from 34.8% (low) to 53.9% (xhigh); Fable 5.1 from 43.3% (low)
  to 57.9% (max).

### 4.2 vals.ai Terminal-Bench 4.0 (one harness for every model)

- [P] vals.ai, "Updated 11/4/2026": "All models were benchmarked using
  mini-swe-agent, a minimal, model-agnostic agent harness. The model is given
  the task instruction and a single tool, bash". avg@3, no step or cost
  limit, 8-hour time limit, Daytona sandboxes. Note: vals.ai used **Terminus
  2 for 2.1** and **mini-swe-agent for 4.0**: "Our Terminal-Bench 2.1 results
  used the Terminus 2 harness; Terminal-Bench 4.0 uses mini-swe-agent."
- [P] Top rows: Opus 5.5 65.15%, Sonnet 5.5 64.14%, Kimi K3.1 Pro 63.64%,
  Gemini 4 Carbon 63.13%, GPT-6 Astra 59.60%, Fable 5.1 58.08%.
- [O] Cross-runner comparison, vendor harness (tbench.ai) vs bash-only
  mini-SWE-agent (vals.ai), same model, TB 4.0. These differ in runner,
  trials (5 vs 3 per task), sandbox and in some cases effort, so read
  differences under about 3 points as noise:

| Model | tbench.ai: harness, effort, score | vals.ai: mini-SWE-agent | Vendor harness minus mini |
|---|---|---|---|
| Opus 5.5 | Claude Code, max, 64.85 | 65.15 | -0.3 |
| Sonnet 5.5 | Claude Code, max, 61.82 | 64.14 | -2.3 |
| GPT-6 Astra | Codex, max, 58.18 | 59.60 | -1.4 |
| Fable 5.1 | Claude Code, max, 57.88 | 58.08 | -0.2 |
| GPT-6.1 Sol | Codex, max, 58.18 | 55.05 | +3.1 |
| Opus 5 | Claude Code, xhigh, 53.94 | 53.53 | +0.4 |
| GPT-6 Sol | Codex, max, 49.39 | 44.44 | +5.0 |
| Fable 5 | Claude Code, max, 44.55 | 41.41 | +3.1 |
| GLM-5.3 | Claude Code, max, 41.82 | 38.89 | +2.9 |
| GPT-5.6 Sol | Codex, max, 37.27 | 37.88 | -0.6 |
| Grok 4.7 | Grok Build, xhigh, 37.58 | 28.79 | +8.8 |
| GLM-5.3-Flash | Claude Code, none, 35.76 | 37.37 | -1.6 |
| Qwen3.8-Max-0902 | Claude Code, max, 26.97 | 38.89 | -11.9 |
| Opus 4.8 | Claude Code, max, 23.64 | 23.23 | +0.4 |
| GPT-5.6 Terra | Codex, max, 21.52 | 22.73 | -1.2 |
| Grok 4.6 | Grok Build, high, 20.30 | 17.17 | +3.1 |
| *Control:* Gemini 3.8 Flash | mini-SWE-agent, high, 19.09 | 19.70 | -0.6 (same harness, different runner) |

- [O] 10 of 16 pairs are within 3 points; 13 of 16 within 3.1. The
  exceptions are Grok 4.7 (+8.8 in xAI's own harness), GPT-6 Sol (+5.0 in
  Codex) and Qwen3.8 Max (-11.9 when run in Claude Code, a harness not
  built for it). The control row (same harness, two runners) agrees within
  0.6 points, which suggests the runner differences are modest. This is a
  comparison we built from two public boards, not a controlled experiment.

### 4.3 Terminal-Bench 2.1 (official board) and vals.ai 2.1

- [P] Official 2.1 board (22 rows, updated Sep 3, 2026), same-model pairs:
  Fable 5: Claude Code (xhigh) 83.82 vs Terminus 2 (high) 80.45; GPT-5.5:
  Codex (xhigh) 83.15 vs Terminus 2 (xhigh) 77.98; Opus 4.7: Claude Code
  (max) 68.90 vs Terminus 2 (max) 66.07; Gemini 3 Pro: Terminus 2 73.93 vs
  Gemini CLI 65.84; Gemini 3.1 Pro: Gemini CLI 65.84 vs Terminus 2 65.62.
  (Fable 5 pair differs in effort.) These confirm and extend round 1's two
  rows in `track3-benchmarks.md`.
- [P] vals.ai 2.1 ("Updated 10/1/2026"), one third party, one runner, same
  model: Claude Opus 4.8, Terminus 2 71.91% vs Claude Code 69.66%.
- [O] Cross-runner warning: Opus 4.8 + Claude Code is 78.88 (high) on the
  official 2.1 board and 69.66 on vals.ai 2.1. The same model and harness
  differ by about 9 points between runners (effort and run setup not
  matched). That is as large as many "harness effects".

### 4.4 Terminal-Bench 2.0 (official board, the widest same-model spreads)

- [P] 142 rows, "seeded from tbench.ai", updated Aug 28, 2026. 73 rows carry
  `verified: true` in the data, 69 `false`.
- [P] Same-model spreads (all rows; verified rows in brackets):

| Model | Lowest → highest (agents) | Rows flagged verified |
|---|---|---|
| Claude Opus 4.6 | Claude Code 58.0 → Meta-Harness 76.4 (9 agents) | Terminus 2 62.9, Claude Code 58.0 |
| Claude Opus 4.5 | OpenCode 51.7 → Droid 63.1 (8) | Terminus 2 57.8, Claude Code 52.1, OpenHands 51.9 |
| GPT-5.3-Codex | Terminus 2 64.7 → SageAgent 78.4 (9) | Simple Codex 75.1, Terminus 2 64.7 |
| GPT-5.5 | clnkr 66.1 → NexAU-AHE 84.7 (4) | Codex CLI 82.2 |
| Claude Haiku 4.5 | OpenHands 13.9 → Goose 35.5 (5) | Mini-SWE-Agent 29.8, Terminus 2 28.3, Claude Code 27.5, OpenHands 13.9 |
| GPT-5 | Mini-SWE-Agent 33.9 → Codex CLI 49.6 (4) | all four |
| Claude Sonnet 4.5 | Claude Code 40.1 → CAMEL-AI 46.5 (6) | Terminus 2 42.8, OpenHands 42.6, Mini-SWE-Agent 42.5, Claude Code 40.1 |
| Gemini 2.5 Pro | OpenHands 16.4 → Terminus 2 32.6 (4) | all four |

- [P] ForgeCode (81.8% on Opus 4.6 in Meta-Harness's Table 7) is not on the
  current 2.0 data. Terminal-Bench's "Leaderboard Integrity Update" (Apr 19,
  2026): "ForgeCode's agent begins by constructing an AGENTS.md file. In
  multiple instances, their agent curls the solution from the internet and
  includes it in its AGENTS.md. We have rescored those trials to 0." The
  same post records two submissions removed for cheating (OB-1 "stored
  encrypted solutions in their agent binary"; Pilot "uploaded the tests/
  folder"). https://www.tbench.ai/news/leaderboard-integrity-update
- [S] A blog says ForgeCode fell "From #1 to 14th" and was later removed;
  not confirmed on tbench.ai.
- [O] Two patterns. Claude Code is the lowest or near-lowest harness for
  every Anthropic model on 2.0 (Opus 4.6, Sonnet 4.5, Haiku 4.5) and below
  the benchmark's own Terminus 2 in verified rows. Lab harnesses are not
  tuned to this benchmark; third-party harnesses often are (Meta-Harness and
  AHE both optimise directly on it). Among verified rows only, spreads
  shrink: Opus 4.6 4.9 points, Opus 4.5 5.9, Sonnet 4.5 2.7, but GPT-5 15.7
  and Gemini 2.5 Pro 16.2 (older models).

## 5. Vendor-run head-to-heads (label as vendor claims)

### 5.1 Factory, Terminal-Bench 4 (Droid 1.0, Oct 29, 2026)

- [P, vendor claim] "Terminal-Bench 4, all tasks, default time limits, run
  October 23–28, 2026." Three trials per task. "High reasoning was chosen as
  it is the most popular reasoning option on our platform." Versions:
  codex@0.163.0, claude-code@2.1.306, cursor-cli@2026.10.19-6bbf2c4,
  devin@3000.11.92, opencode@2.1.2; no Droid version listed.
  https://factory.com/news/frontier-harness
- [P] GPT-6.1 Sol: Droid 57.6%, Codex 54.0%, OpenCode 51.0%, Devin 45.0%.
  Opus 5.5: Droid 65.2%, Cursor 62.1%, OpenCode 62.1%, Devin 59.6%, Claude
  Code 57.6%. (Matches `round5-platforms-research.md` §4.8.)
- [P] Adjustments in the post: Opus tasks stopped by Anthropic moderation
  were rerun on Opus 5; a Devin task "was counted as passed if Codex passed
  it" (about 4.7 tasks per trial); Cursor tokens estimated for two trials.
- [O] Against the official board: Claude Code + Opus 5.5 is 64.8% ± 3.1 at
  max effort on tbench.ai and 57.6% at high effort in Factory's run. Codex +
  GPT-6.1 Sol is 58.2% at max on tbench.ai and 54.0% at high for Factory.
  Effort differs, so these are not contradictions, but Factory's winning
  margin (Droid +7.6 over Claude Code) is the same size as the gap between
  Factory's Claude Code number and the official one. The post does not
  mention the official board.

### 5.2 GitHub, Copilot CLI harness parity study (Jun 25, 2026)

- [P, vendor claim] Shibani Basava and Carlos Castro. Copilot CLI vs "Claude
  Code for Sonnet 4.6 and Opus 4.7, and Codex CLI for GPT‑5.4 and GPT‑5.5" on
  SWE-bench Verified, SWE-bench Pro, SkillsBench, TerminalBench 2.0 and
  internal Win-Hill. Reasoning effort medium; "no tool search, no MCP
  servers" except TerminalBench 2.0; pass@1.
- [P] "These results reflect effective parity, since the differences in
  either direction are within the variance."
- [P] Method detail worth flagging: "We ran each agent-model combination at
  least five times", and for benchmarks under 100 instances "five
  independent runs were conducted, and the best scored run is reported."
- [P] Per-benchmark numbers appear only in charts. Chart alt text, SkillsBench
  resolution: "Copilot CLI performed worse for Sonnet 4.6 and Opus 4.7, but
  better for GPT models." Token efficiency on SWE-bench Verified for GPT
  models: "where it did 7% and 4% worse, respectively". This settles the [E]
  flag in `round5-copilot-architecture.md` §7: the SkillsBench sentence is in
  the alt text, not the body.
- [O] The post names no versions for the competing harnesses and does not say
  who ran them. Its message ("our harness is as good as the labs' own") fits
  the independent pattern in §4.2 and §6.1: for strong models, competent
  harnesses land close together.

## 6. Benchmark validity: the measurement under the harness claims

### 6.1 SWE-Bench Pro V2 (Scale AI, arXiv 2610.24206, Oct 16, 2026)

- [P] Soham Dan, Jeff Da and nine others, Scale AI Research. "Agentic
  audits, expert adjudication and blind re-implementation repaired or
  retired 480 of the 731 tasks". Release: 642 tasks (391 repaired, 89
  discarded). Defects include "tests that check behavior the instruction
  never states, instructions that contradict or leak the tests, weak tests,
  and verifier or environment defects".
- [P] Exploits found: with network open, "32 of 642 Claude Opus 5 runs
  (5.0%) contacted code hosts and 25 downloaded the task's own repository";
  agents forged Go dependencies outside the patch; "a scripted agent that
  edits no source file and replaces python3 with a script printing PASSED
  scores 1" under the original in-sandbox grading.
- [P] Results: Opus 5 (xhigh) in Claude Code 99.4%; Fable 5.1 (high) 99.1%;
  Kimi K3 (max, mini-swe-agent) 97.5%; GPT-6 Astra (high, Codex) 96.9%;
  Haiku 5.5 87.2%. 51-task Hard split: 52.9% to 98.0%.
- [P] **§4.5 "Effect of the agent harness"** (GLM-5.3, Kimi K3, Inkling;
  mini-swe-agent, Pi, OpenCode; all 642 tasks): "Accuracy barely moves ...
  across the 642 tasks every run attempted the task explains 32% of the
  variance in solved-or-failed, the model 2.7% and the scaffold 0.3%." Table
  3 spreads: GLM-5.3 0.9 points, Kimi K3 1.7, Inkling 7.5 (Pi trailing). What
  the scaffold changes is cost: "Kimi K3 spends 1.3M tokens per solved task
  under Pi against 2.6M under mini-swe-agent".
- [O] Strongest single counterweight to the "harness dominates" story, from
  the benchmark's own maintainer. Limits: open-weight models only, and V2 is
  near saturation (87 to 99%), which compresses every difference, model and
  harness alike.

### 6.2 SWE-Bench Pro Verified (arXiv 2609.08149, Sep 2026)

- [P] Pujun Zheng, Zixin Shang, Shufan Jiang, Wenhui Tian, Dongsheng Zhu,
  Zerun Ma, Dingbo Yuan, Qi Zhang. v1 Sep 8, 2026; v2 Sep 16; v3 Oct 9.
- [P] Abstract: SWE-Bench Pro's "evaluation is undermined by two sources of
  unreliability: reward hacking, enabled by leakage of gold solutions or
  hidden evaluation information, and task quality issues, including
  misleading problem statements and improperly scoped tests."
- [P] Numbers: GLM-5.2 "decreases from 78.80% to 57.32%, a drop of 21.48
  percentage points" once leakage channels are blocked; 186 passes became
  failures and 15 failures became passes. Baseline trajectories showed
  "local answer leakage for at least 103 tasks and network answer leakage
  for 49 tasks". 102 instances refined. All runs used mini-swe-agent.
- [R] The task brief described this as a preprint "about misgraded trials".
  The paper is about reward hacking (agents finding answers) and task defects
  (bad specs and tests), not grader error rates on trials. The "about a
  third of trials misgraded" figure circulating in trade press is attributed
  to a separate Datacurve audit (May 2026) [S, aiweekly.co]; we did not find
  the primary document.

### 6.3 Earlier-round caveats (cite, not refetched)

- `track3-benchmark-critiques.md`: contamination (SWE-bench+ 32.67% solution
  leakage; SWE-Bench Illusion file-path recall up to 76%), realism (Django
  about half of Verified), saturation, vendor self-reporting (llm-stats: 0 of
  116 Verified scores independently verified on Sep 30, per round 2 §3).
  Note: its §7 repeats the "50.2%–55.4%" Opus 4.5 range, which is [R].
- `round2-evals-and-benchmarks.md` §6.3: METR could not get a robust GPT-5.6
  Sol time horizon because of cheating ("We do not consider any of these
  numbers to represent a robust measurement").
- [O] Every benchmark used in harness comparisons above (SWE-bench Verified,
  SWE-bench Pro v1, Terminal-Bench 2.0) has a documented leakage or hacking
  problem. A harness that lets the agent reach the internet or the git
  history can "win" by finding answers. Harness differences of a few points
  on these boards cannot be separated from that.

## 7. Earlier-round deltas (cited from our files)

| Same model, different harness | Delta | Source in our files | Tag |
|---|---|---|---|
| GPT-4o, scaffolds on Verified | 23% → 33.2% | `track3-benchmarks.md` (Epoch) | [S] round 1 |
| Claude 3.7, generic vs custom | 62.3% → 70.2% | same | [S] round 1 |
| DeepSeek R1-0528, scaffold switch | 33% → 57.6% | same | [S] round 1 |
| Opus 4.5, three harnesses on SWE-bench Pro, "50.2%–55.4%" | | `track3-benchmarks.md`, `track3-benchmark-critiques.md` §7 | **[R]** (round 2 and §1.1 here) |
| Opus 4.5 Anthropic setup vs SEAL, SWE-bench Pro | 52.0% vs 45.89% (6.1) | `round2-evals-and-benchmarks.md` §3 | [P] |
| GPT-5.2-Codex, OpenAI setup vs SEAL, SWE-bench Pro | 56.4% vs 41.04% (15.4) | same | [P]; OpenAI does not name its harness |
| CORE-Bench, Opus 4.5 after grader fixes and scaffold change | 42% → 95% | `round2-evals-and-benchmarks.md` §1 | [V]; part of the jump is grading |
| Epoch v2.0.0 scaffold upgrade | "model performance improving significantly" | same §3 | [P] |
| ARC-AGI-3, GPT-5.6 Sol, retained reasoning plus compaction | 13.3% → 38.3% | `round5-openai-codex.md` §8 | [P], vendor claim |
| Qwen Code, seven harness versions, Qwen 3.7 Max, Verified | 76.40%–77.80% | `round5-oss-terminal.md` §7 | [P], vendor claim |
| Hashline edit format, Grok Code Fast 1 | 6.7% → 68.3% | `round5-convergence-standards.md` §2.4 | [P], single blog, internal inconsistencies noted there |

## 8. Other checks requested

### 8.1 Barbaste et al., arXiv 2609.00006

- [P] Title: "Harness Engineering: Anatomy, Architecture, and Evolution of
  Coding Agents -- A Source-Code Study of Eleven Systems". Paul Barbaste,
  Tristan Darrigol, Germain Vu, Tom Wiltberger. arXiv page: "[Submitted on
  15 Jul 2026]", v1 only; the HTML header reads "arXiv:2609.00006v1 [cs.SE]
  15 Jul 2026".
- [O] ID/date inconsistency: arXiv assigns the identifier when a paper is
  announced, and the "Submitted" date is the upload date. A 2609 identifier
  with a Jul 15 upload fits a paper held in moderation for about seven weeks
  and announced in early September (the low number 00006 fits the start of a
  month). We cannot confirm a hold from the page. The paper also refers to an
  earlier "April edition" of the study that is not this arXiv record.
- [P] Exact wording: "Observation 1. The eleven systems span
  three orders of magnitude in code size while targeting similar tasks, yet
  loop sophistication does not predict benchmark performance. Mini-SWE-Agent's
  minimal linear loop achieves reported results in the same range as
  OpenHands's event-sourced conversation engine".
- [R, corrected in verification pass] Earlier text claimed an internal
  inconsistency: Recommendation 1 cites "Observation 5 (loop sophistication
  does not predict benchmark performance)" while the observation is
  labelled Observation 1. That wording appears only in arXiv's HTML
  rendering. The PDF (the authoritative version) reads "Evidence:
  Observation 1 (loop sophistication does not predict benchmark
  performance)". The "5" is an HTML conversion artifact, not an error by the
  authors. In both versions Observation 5 is about persistent memory.
- [P] The evidence is self-reported scores, not a run: "The April edition of
  this study tabulated SWE-Bench Verified scores per system. We have removed
  them from the comparison table: the available figures are self-reported,
  obtained on different model generations and configurations". And: "Whether
  the production scaffolding produces measurable improvements on the same
  benchmark under matched conditions is an open question that this study
  does not answer".
- [O] Our synthesis's summary ("loop sophistication does not predict
  benchmark results") is accurate if it keeps "benchmark performance" and
  notes the numbers are self-reported. Upgrade from [P\*] to [P].

### 8.2 Rombaut, "Inside the Scaffold", arXiv 2604.03515

- [P] Benjamin Rombaut, v1 Apr 3, v2 Apr 10, 2026. §4.2.1: "Tool counts range
  from 0 (Aider) to 37 action classes (Moatless Tools), but raw counts
  obscure a convergence in capability categories (Table 5). Despite this
  range, the same four core capability categories (read, search, edit,
  execute) appear across all LLM-driven agents (as classified in Section
  4.1.2). A fifth category, validate ... appears only in Moatless Tools".
- [O] The quote in `round5-convergence-standards.md` and the synthesis is
  verbatim. Upgrade from [P\*] to [P].

### 8.3 Agent Retrieval Bench, arXiv 2607.24882

- [P] Bowen Qin, Yi Xie, submitted Jul 27, 2026. Abstract: "No single
  retrieval family dominates: Qwen3-Embedding-4B has the best sample-weighted
  MRR on positive samples, Qwen3-Embedding-8B the best Recall@20, and RepoMap
  the best budgeted context yield at 8K tokens, with task-level winners
  differing substantially." Also: "Logged trajectories also miss every gold
  file on 27-35 percent of samples." 427 samples, 25 repositories.
- [O] Quote verbatim; upgrade from [P\*] to [P]. Note it measures file
  retrieval, not end-to-end task success.

## 9. Table: same model, different harness

Rows sorted by source type. "Δ" is highest minus lowest harness unless
stated. Benchmarks with known leakage problems are marked †.

| # | Model | Benchmark | Harnesses compared | Scores | Δ (pts) | Who ran it | Source | Tag |
|---|---|---|---|---|---|---|---|---|
| 1 | Qwen3.6-35B-A3B (4-bit) | SWE-bench Verified†, 169 tasks, 20k window | Yuj control vs Yuj treatment | 43 vs 72 solved; F2PF 28% vs 49% | +17.2 resolution | Author (built Yuj) | arXiv 2608.26218 | [P] |
| 2 | Qwen3.6-35B-A3B | Same, 262k window | same | 102 vs 101 solved | -0.6 | same | same | [P] |
| 3 | Qwen3.6-35B-A3B | SWE-bench Pro†, 316 tasks, 49k window | same | 31 vs 72 solved | +13.0 | same | same | [P] |
| 4 | Devstral / Nemotron / Qwen3.8 | Verified†, 20k window | same | 22→53 / 16→25 / 32→54 solved | +18.3 / +5.3 / +13.0 | same | same | [P] |
| 5 | GLM-5.1 | Verified† subset100 | H1 vs H2 vs H3 | 52.5 / 56.5 / 65.5 | 13.0 | Authors (position paper) | arXiv 2605.23950 Table 2 | [P] |
| 6 | GPT-5.4 | same | same | 55.0 / 58.5 / 63.5 | 8.5 | same | same | [P] |
| 7 | Kimi K2.6 | same | same | 52.0 / 59.0 / 60.5 | 8.5 | same | same | [P] |
| 8 | GLM-5.3 (thinking) | SWE-Bench Pro V2, 642 tasks | mini-swe-agent / Pi / OpenCode | 95.6 / 96.6 / 96.4 | 0.9 | Scale AI (benchmark owner) | arXiv 2610.24206 Table 3 | [P] |
| 9 | Kimi K3 (max) | same | same | 97.5 / 96.0 / 97.7 | 1.7 | same | same | [P] |
| 10 | Inkling (xhigh) | same | same | 89.9 / 84.1 / 91.6 | 7.5 | same | same | [P] |
| 11 | Claude Opus 4.6 | Terminal-Bench 2.0† | Claude Code ... Meta-Harness (9 agents) | 58.0 → 76.4 | 18.4 (4.9 among verified rows) | Mixed; most top rows unverified submissions | tbench 2.0 data; Meta-Harness Table 7 | [P] |
| 12 | Claude Opus 4.6 | Terminal-Bench 2.0† | Terminus-KIRA (base) / Capy (best reproducible hand-built) vs Meta-Harness | 74.7 / 75.3 vs 76.4 | 1.7 over base; 1.1 over Capy | Stanford (search and eval on same tasks) | arXiv 2603.28052 | [P] |
| 13 | Claude Haiku 4.5 | Terminal-Bench 2.0† | OpenHands ... Goose (5) | 13.9 → 35.5 | 21.6 | Mixed | tbench 2.0 data | [P] |
| 14 | Claude Opus 4.5 | Terminal-Bench 2.0† | OpenCode ... Droid (8) | 51.7 → 63.1 | 11.4 (5.9 verified) [11.5 was an arithmetic slip, fixed] | Mixed | tbench 2.0 data | [P] |
| 15 | GPT-5.3-Codex | Terminal-Bench 2.0† | Terminus 2 ... SageAgent (9) | 64.7 → 78.4 | 13.7 | Mixed | tbench 2.0 data | [P] |
| 16 | GPT-5 | Terminal-Bench 2.0† | Mini-SWE-Agent ... Codex CLI (4, all verified) | 33.9 → 49.6 | 15.7 | Mixed | tbench 2.0 data | [P] |
| 17 | GPT-5.5 | Terminal-Bench 2.1 | Terminus 2 vs Codex | 77.98 vs 83.15 | 5.2 | tbench board | tbench 2.1 data | [P] |
| 18 | Opus 4.7 | Terminal-Bench 2.1 | Terminus 2 vs Claude Code | 66.07 vs 68.90 | 2.8 | tbench board | tbench 2.1 data | [P] |
| 19 | Gemini 3 Pro | Terminal-Bench 2.1 | Gemini CLI vs Terminus 2 | 65.84 vs 73.93 | 8.1 | tbench board | tbench 2.1 data | [P] |
| 20 | Claude Opus 4.8 | Terminal-Bench 2.1 | Claude Code vs Terminus 2 | 69.66 vs 71.91 | 2.3 | vals.ai (one runner) | vals.ai TB 2.1 | [P] |
| 21 | 16 frontier models | Terminal-Bench 4.0 | Vendor harness (tbench) vs mini-SWE-agent (vals) | see §4.2 | 10 of 16 within ±3; outliers +8.8, +5.0, -11.9 | Two runners | tbench 4.0 data + vals.ai TB 4.0 | [P] data, [O] pairing |
| 22 | GPT-5.4 (high) | Terminal-Bench 2† | Seed vs AHE-evolved harness | 69.7 → 77.0 | 7.3 | AHE authors | arXiv 2604.25850 | [P] (model [P\*]) |
| 23 | gpt-5.2-codex | Terminal-Bench 2.0† | LangChain DeepAgents before/after | 52.8 → 66.5 | 13.7 | LangChain (vendor) | `round2-harness-reference-designs.md` §8 | [P], vendor claim |
| 24 | Claude Opus 4.5 | SWE-bench Pro† public | SEAL / Claude Code / Cursor / Auggie | 45.89 / 49.75 / 50.21 / 51.80 | 5.9 (2.05 among products) | Scale (SEAL); Augment (the three products) | Augment post; round 2 §3 | [P], Auggie vendor claim |
| 25 | Claude Opus 4.5 | SWE-bench Pro† | SEAL → Claude Code "45.9 → 55.4" | | "+9.5" | | arXiv 2605.23950 via Morph | **[R]** |
| 26 | Opus 5.5 | Terminal-Bench 4 | Claude Code / Devin / OpenCode / Cursor / Droid | 57.6 / 59.6 / 62.1 / 62.1 / 65.2 | 7.6 | Factory (vendor, high effort) | factory.com/news/frontier-harness | [P], vendor claim |
| 27 | GPT-6.1 Sol | Terminal-Bench 4 | Devin / OpenCode / Codex / Droid | 45.0 / 51.0 / 54.0 / 57.6 | 12.6 (Devin adjusted upward) | Factory | same | [P], vendor claim |
| 28 | Sonnet 4.6, Opus 4.7, GPT-5.4, GPT-5.5 | Verified, Pro, SkillsBench, TB 2.0, Win-Hill | Copilot CLI vs Claude Code / Codex CLI | charts only; "effective parity" | within variance (vendor) | GitHub (vendor) | github.blog, Jun 25, 2026 | [P], vendor claim |
| 29 | Grok 4 | SWE-bench Verified† | SWE-agent → xAI scaffold | 58.6 → 72–75 | 14–16 | Vals AI, xAI | via arXiv 2605.23950 Table 1 | [P\*] |
| 30 | Sonnet 4.5 / GPT-5 Medium | SWE-bench Verified Mini† | HAL Generalist vs SWE-Agent | 34 vs 68 / 12 vs 46 | 34 / 34 | HAL | via arXiv 2605.23950 §4.1 | [P\*] |
| 31 | Qwen 3.7 Max | SWE-bench Verified† | Seven Qwen Code versions | 76.40–77.80 | 1.4 | Qwen (vendor) | `round5-oss-terminal.md` §7 | [P], vendor claim |
| 32 | GPT-4o / Claude 3.7 / DeepSeek R1-0528 | SWE-bench Verified† | Epoch scaffold comparisons | 23→33.2 / 62.3→70.2 / 33→57.6 | 10.2 / 7.9 / 24.6 | Epoch | `track3-benchmarks.md` | [S] |

## 10. What a presenter can honestly claim [O]

**Safe to say.**

1. A benchmark score belongs to a model plus a harness plus settings. Every
   independent source agrees on this, including the papers on both sides
   (2605.23950, 2608.26218, Scale's V2 paper: "we report them per system,
   defined as the combination of the three").
2. Changing only the harness can move results a lot when the harness fixes
   a real constraint. Best example: 43 vs 72 tasks solved by the same
   open-weight model when the harness manages a small context window
   (2608.26218), and the same change doing nothing when the window is large.
3. On a single public leaderboard, one model can score anywhere from 58% to
   76% depending on the agent (Opus 4.6, Terminal-Bench 2.0). Say in the same
   breath that the top rows are mostly unverified submissions tuned to that
   benchmark, and that the board had to rescore one harness for downloading
   answers.
4. For current frontier models on well-graded tasks, good harnesses land
   close together. Scale's V2 paper: scaffold explains 0.3% of outcome
   variance against 2.7% for the model and 32% for the task. Terminal-Bench
   4.0: Claude Code and Codex score within about 3 points of a bash-only
   harness for most frontier models.
5. Vendor head-to-heads each show the vendor's harness winning or tying
   (Factory, GitHub, Augment). Treat them as claims; runner and effort
   differences between boards are as large as the claimed margins.
6. Effort settings move scores as much as harness choice: Opus 5 in Claude
   Code goes from 34.8% (low) to 53.9% (xhigh) on Terminal-Bench 4.0.

**For a Copilot-only bank, the relevant reading.** The measured evidence does
not support "you are losing 10 to 20 points by using Copilot instead of
Claude Code or Codex". GitHub claims parity (vendor), and the independent
data says competent harnesses on frontier models are within a few points of
each other. The larger levers inside the harness are the ones a team
controls: context management on long tasks, verification before finishing
(2605.23950's H2→H3 gain; Scale's finding that "testing after the last edit
roughly doubles the odds of solving"), the model and effort chosen, and
what the agent is allowed to reach (benchmarks show agents fetch answers
when the network is open).

**Do not say.**

- "Same model scores 45.9% vs 55.4% depending on harness" [R]. Use 45.89%
  (SEAL) vs 49.75% (Claude Code) vs 51.80% (Auggie, vendor claim) instead.
- "The harness matters more than the model" as a general rule. The one
  controlled grid that shows it used near-tied models, 100 tasks and a weak
  baseline harness; the benchmark owner's own study found the reverse for
  open-weight models.
- "Terminal-Bench 4.0 shows harness X beats harness Y on the same model."
  The official 4.0 board has no such rows.
- Any harness delta from SWE-bench Verified or Terminal-Bench 2.0 without
  noting the leakage and hacking problems on those boards.
- "Barbaste et al. measured that loop sophistication doesn't matter." They
  compared self-reported scores and say the matched comparison "is an open
  question that this study does not answer".

## 11. Could not verify

- The live Morph page (Vercel checkpoint, then HTTP 429); used Wayback
  snapshots of Apr 3 and Jul 1, 2026.
- Whether ForgeCode was removed from Terminal-Bench 2.0 or only rescored. The
  integrity post says rescored; the current data has no ForgeCode row; the
  "removed" claim is [S].
- The meaning of the `verified` flag in Terminal-Bench 2.0 data (assumed to
  mark rows the board checked; not documented on the pages read).
- vals.ai's per-model reasoning effort for the TB 4.0 headline rows ("labelled
  with each provider's own setting" in its effort chart; not given per row).
- HAL, Epoch "Why benchmarking is hard", Vals AI Grok 4 and Vercel numbers
  quoted in 2605.23950, left at [P\*].
- A primary source for the "about a third of SWE-Bench Pro trials misgraded"
  claim (attributed to Datacurve, May 2026) [S].
- The arXiv moderation-hold explanation for 2609.00006's ID is inference.
- GitHub parity study per-benchmark numbers (charts only).

## Verification pass (2026-11-04)

Adversarial re-check against primary pages, done the same day. Tags above
were updated in place where noted.

**Checked and confirmed [P]**

1. arXiv 2605.23950: title, six authors, v1 only, May 7, 2026. §2.1
   sentence (45.9% SEAL vs 55.4% Claude Code), Table 1 row "+9.5pp (45.9% →
   55.4%)", Table 2 (all nine cells), "13.0 ... 8.5 points each", 7.80x
   aggregate with 8.72x and 6.76x run-level, "We do not claim that the
   7.80× ratio is universal", costs ($34.19 vs $22.19, 18.9M vs 9.7M tokens,
   $215.79 total), thesis and closing sentences (both in the abstract), and
   the §4.1 "roughly twofold" claim (9.5 vs 4.9 points).
2. Augment post: Auggie 51.80%, Cursor 50.21%, Claude Code 49.75%, all
   Opus 4.5, 731 problems, run by Augment; SWE-Agent 45.89% taken from
   Scale's leaderboard (Jan 2026). Feb 4, 2026, last updated Jun 18, 2026.
   No 55.4 on the page.
3. Morph Apr 3, 2026 Wayback capture (fetched by curl): Agent Systems table
   with Claude Code / Opus 4.5 / 55.4% / Anthropic, "Scores are
   self-reported by each team", SEAL table with Opus 4.5 45.9% first and
   GPT-5.2 Codex 41.0% sixth (the paper's 4.9-point range). WarpGrep chart
   shows Opus 4.6 55.4 → 57.5 (MiniMax 2.5 also has a 55.4 baseline). Jul 1
   capture: agent table gone, DeepSeek-V4-Pro-Max at 55.4%.
4. arXiv 2608.26218: author, Aug 26, 2026; all Table 2 numbers; 262k
   results (102 vs 101, "-0.3 percentage points (95% interval [-4.5,
   +3.9])", Pro 101 vs 99, FeatureBench 23.9% → 30.7%, 5 vs 5); 43k window
   76 → 87, p=0.0614; Devstral, Nemotron, Qwen3.8 numbers; 87.6% agreement,
   kappa 0.66, GPT-5.5, mini-SWE-agent v2.2.8; 3,280 vs 6,517 turns, 1.3 vs
   4.6 hours. §9 rows 1 to 4 arithmetic checks out (n=169 for Verified).
5. arXiv 2610.24206 (Scale, Oct 16, 2026): 480 of 731, 642 / 391 / 89, the
   32 of 642 Opus 5 runs, the python3 PASSED exploit, Table 2 headline
   scores, Hard split 52.9 to 98.0, the §4.5 variance sentence (Appendix B:
   31.7%, 2.65%, 0.29%), Table 3 values, 1.3M vs 2.6M tokens, "roughly
   doubles the odds of solving", "defined as the combination of the three".
   GLM-5.3's stated 0.9 spread vs 1.0 from rounded cells is rounding.
6. Terminal-Bench "Leaderboard Integrity Update": ForgeCode quotes
   verbatim; OB-1 and Pilot "removed from the leaderboard"; ForgeCode
   rescored, not removed. Date Apr 19, 2026 confirmed on tbench.ai/news (the
   post page itself shows no date).
7. Meta-Harness (2603.28052): authors and affiliations, Mar 30, 2026, Table
   7 (all 17 rows), the ForgeCode reproduction sentence, 7.7 points / 4x,
   4.7 points / five held-out models, ~80 lines on Terminus-KIRA, 7 of 89
   tasks, search and evaluation on the same 89 tasks.
8. Factory (Oct 29, 2026): run dates, three trials, high-effort rationale,
   five harness versions, every score for GPT-6.1 Sol and Opus 5.5, the
   moderation reruns on Opus 5, Devin rule "an average of 4.7 tasks per
   trial", Cursor token estimate. No mention of the official board.
9. GitHub (Basava and Castro, Jun 25, 2026): harness and model list,
   medium effort, tool search / MCP exceptions for TerminalBench 2.0,
   "effective parity", "at least five times", "best scored run is
   reported", both alt-text quotes. No competitor versions named.
10. vals.ai TB 4.0 ("Updated 11/4/2026"): methodology quotes and all 17
    scores used in §4.2 match. The board also has a second Qwen 3.8 Max row
    (34.34%, no 0902 suffix); §4.2 correctly pairs the 0902 row. Effort is
    per model in a chart only, no effort column in the table.
11. vals.ai TB 2.1 ("Updated 10/1/2026"): Opus 4.8 Terminus 2 71.91%,
    Claude Code 69.66%; no effort stated.
12. arXiv 2609.08149: authors, v1 Sep 8, v2 Sep 16, v3 Oct 9; "two sources
    of unreliability"; GLM-5.2 78.80% → 57.32% (21.48); 186 and 15; 103 and
    49 leakage tasks; 102 refined; all runs on mini-swe-agent.
13. arXiv 2609.00006: title, four authors, "Submitted on 15 Jul 2026", v1
    only; comments field: "Second, substantially expanded edition of an
    April 2026 study". Observation 1 quote verbatim (curly apostrophes in
    the source); "We have removed them from the comparison table" footnote
    verbatim; "is an open question that this study does not answer"
    verbatim (§13.4).
14. arXiv 2604.03515 (Rombaut, v1 Apr 3, v2 Apr 10) and 2607.24882 (Qin and
    Xie, Jul 27; 427 samples, 25 repos): quotes verbatim.
15. arXiv 2604.25850 (AHE): abstract quote verbatim; the abstract does not
    name the model, so GPT-5.4 stays [P\*].
16. TB 4.0 Opus 5.5 / Claude Code / max 64.8% ± 3.1 and Sonnet 5.5 61.8%:
    corroborated only through a third-party mirror of the board
    (developersdigest.tech, Oct 17 snapshot) [S for this pass].

**Corrected**

- §1.3: LLM Stats scores were listed in the wrong model order (implied
  GPT-5.4 = 45.4). Paper: Kimi K2.6 45.4, GLM-5.1 45.3, GPT-5.4 44.6.
- §2: the McNemar figures are in Table 7 and §3.5, not Table 2; the
  "Because changing the harness ..." sentence is from the abstract, not the
  Conclusion.
- §3 and §9 row 12: Terminus-KIRA (74.7) is not the strongest hand-built
  harness in Table 7; Capy is (75.3). Meta-Harness's margin is 1.1 over
  Capy, 1.7 over the Terminus-KIRA base. The paper reports no confidence
  intervals; the ±2.4 to 2.6 figure is the leaderboard's.
- §8.1: the "Observation 5" inconsistency in Barbaste is an arXiv HTML
  artifact. The PDF's Recommendation 1 cites Observation 1. Downgraded to
  [R].
- §9 row 14: Opus 4.5 spread is 11.4 points (63.1 - 51.7), not 11.5.
- §1.1: the "Jun 28 snapshot" is the Jul 1, 2026 Wayback capture of a page
  marked "Updated June 28, 2026". Added that Augment's SWE-Agent baseline
  comes from Scale's leaderboard, not Augment's own run.

**Could not verify in this pass**

- The official tbench.ai board data (4.0, 3.0, 2.1, 2.0 rows, the
  `verified` flag, 142 / 73 / 69 counts, Oct 23 updated_at). The 4.0 page
  renders no rows to a fetcher, the Harbor endpoint returns HTTP 400 without
  parameters, and a direct download was refused. All §4.1, §4.3 (official
  rows) and §4.4 numbers rest on the original agent's read; treat as [E]
  until rechecked in a browser.
- The live Morph page (not retried; Wayback captures were read).
- HAL, Epoch, Vals Grok 4 and Vercel numbers inside 2605.23950 (still
  [P\*]).
- The Datacurve "a third of trials misgraded" claim (still [S]).
- GitHub per-benchmark numbers (charts only).

**Follow-up check (2026-11-05)**

- 2026-11-05: in arXiv 2608.26218 Table 9 the "1.3 vs 4.6" figures are
  solver wall time in hours (column "solver wall time (hours) C / T"), not
  a compute measure. Read the §2 bullet "Treatment used more compute" as
  "treatment ran more model turns and longer wall-clock time".
