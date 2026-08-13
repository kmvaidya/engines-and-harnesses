---
url: https://ar5iv.labs.arxiv.org/html/2001.08361, https://epoch.ai/blog/estimating-training-compute, https://epoch.ai/blog/backward-forward-FLOP-ratio, https://arxiv.org/abs/2407.21783, https://epoch.ai/data-insights/models-over-1e25-flop, https://arxiv.org/abs/2412.19437, https://en.wikipedia.org/wiki/Cray-1, https://www.nvidia.com/en-us/data-center/h100/
fetched: 2026-08-12
---

# Track 3 — How many FLOPs is one token? (research notes)

## Summary table: FLOPs per token (forward pass, ≈ 2 × active params)

| Model | Total params | Active params/token | FLOPs/token (2N) | Status | Source |
|---|---|---|---|---|---|
| Llama 3.1 405B | 405B (dense) | 405B | **~8.1×10^11** | Official (params); 2N rule standard | [arXiv:2407.21783](https://arxiv.org/abs/2407.21783) |
| GPT-4 (original) | ~1.8T (MoE, 16 experts) | ~280B | **~5.6×10^11** | Unofficial leak (SemiAnalysis) | [SemiAnalysis](https://www.semianalysis.com/p/gpt-4-architecture-infrastructure) via [the-decoder](https://the-decoder.com/gpt-4-architecture-datasets-costs-and-more-leaked/), [McGuinness summary](https://patmcguinness.substack.com/p/gpt-4-details-revealed) |
| DeepSeek-V3 | 671B (MoE) | 37B | **~7.4×10^10** | Official (params); 2N rule standard | [arXiv:2412.19437](https://arxiv.org/abs/2412.19437) |

Training compute totals: Llama 3.1 405B = **3.8×10^25 FLOPs** (official, Meta paper); GPT-4 ≈ **2×10^25 FLOPs** (Epoch AI third-party estimate, listed as 2.1e25 in their table); DeepSeek-V3 ≈ **3.3×10^24 FLOPs** (via 6ND arithmetic below).

---

## 1. The standard approximation: 2N forward, 6N training

**Rule of thumb:** a dense transformer with N parameters does ≈ **2N FLOPs per token in the forward pass** (each parameter participates in one multiply-accumulate = 2 FLOPs). Training adds the backward pass at ≈ 2× the forward cost, so **training ≈ 6N FLOPs per token**, and total training compute C ≈ 6 × N × D (D = training tokens).

- **Kaplan et al., "Scaling Laws for Neural Language Models" (arXiv:2001.08361), Section 2.1 / Table 1** — [https://ar5iv.labs.arxiv.org/html/2001.08361](https://ar5iv.labs.arxiv.org/html/2001.08361):
  - "Evaluating a forward pass of the Transformer involves roughly C_forward ≈ 2N + 2·n_layer·n_ctx·d_model add-multiply operations."
  - "Accounting for the backwards pass (approximately twice the compute as the forwards pass), we then define the estimated non-embedding compute as C ≈ 6N floating point operators per training token."
- **Epoch AI, "Estimating training compute"** — [https://epoch.ai/blog/estimating-training-compute](https://epoch.ai/blog/estimating-training-compute): forward pass ≈ "twice the number of connections" (2N); total training compute ≈ 6 × parameters × tokens.
- **Epoch AI, "Backward-forward FLOP ratio"** — [https://epoch.ai/blog/backward-forward-FLOP-ratio](https://epoch.ai/blog/backward-forward-FLOP-ratio): backward:forward ratio ≈ 2:1 in typical large-batch settings (range 1:1–3:1), justifying the ×3 multiplier on the forward pass.

**What 2N ignores — the attention correction term.** Kaplan's full per-token forward cost is 2N + **2·n_layer·n_ctx·d_model** (attention score computation over the context). Kaplan: "For contexts and models with d_model > n_ctx/12, the context-dependent computational cost per token is a relatively small fraction of the total compute." At long context it stops being small. Concretely, for Llama 3.1 405B (126 layers, d_model = 16,384 — Table 3 of [arXiv:2407.21783](https://arxiv.org/html/2407.21783v3)):

- At 8K context: 2 × 126 × 8,192 × 16,384 ≈ 3.4×10^10 extra FLOPs/token ≈ **+4%** on top of 8.1×10^11.
- At 128K context: 2 × 126 × 131,072 × 16,384 ≈ 5.4×10^11 extra FLOPs/token ≈ **+67%**.

So 2N is a good approximation at short/moderate context and an undercount at long context. It also excludes embeddings, nonlinearities, and normalization (all small).

---

## 2. Concrete figures (each with citation)

### Llama 3.1 405B — official
- Dense transformer, **405B parameters**, trained on **15.6T tokens**: "we pre-trained a flagship model with 405B trainable parameters on 15.6T text tokens" — [arXiv:2407.21783](https://arxiv.org/html/2407.21783v3) (Meta, official).
- Training compute: "our flagship model was pre-trained using **3.8×10^25 FLOPs**, almost 50× more than the largest version of Llama 2" — same paper (official). Independently listed at 3.8e+25 FLOP in Epoch AI's frontier-models table — [epoch.ai/data-insights/models-over-1e25-flop](https://epoch.ai/data-insights/models-over-1e25-flop) (third-party, agrees).
- **Forward FLOPs/token = 2N = 2 × 405×10^9 = 8.1×10^11** (~0.81 TFLOPs per token).
- Sanity check of the 6ND rule: 6 × 405×10^9 × 15.6×10^12 = 6 × 6.318×10^24 = **3.79×10^25** — matches Meta's official 3.8×10^25. The rule works.

### GPT-4 — third-party estimates only (OpenAI disclosed nothing)
- **Training compute ≈ 2×10^25 FLOPs** — Epoch AI estimate (their table lists 2.1e25, "compute estimated using training hardware and training duration") — [epoch.ai/data-insights/models-over-1e25-flop](https://epoch.ai/data-insights/models-over-1e25-flop). **Third-party estimate, not official.**
- **Architecture (unofficial leak, label clearly):** SemiAnalysis reported (July 2023) ~**1.8T total parameters**, 120 layers, MoE with 16 experts (~111B each, 2 routed per token), ~**280B active parameters per token**, "about 560 TFLOPs" per forward pass, ~13T training tokens. Original: [semianalysis.com/p/gpt-4-architecture-infrastructure](https://www.semianalysis.com/p/gpt-4-architecture-infrastructure) (paywalled); figures as relayed by [the-decoder.com](https://the-decoder.com/gpt-4-architecture-datasets-costs-and-more-leaked/) and [patmcguinness.substack.com](https://patmcguinness.substack.com/p/gpt-4-details-revealed): "Each forward pass inference (generation of 1 token) utilizes about 280B parameters and about 560 TFLOPs."
- Note the internal consistency: 2N on active params = 2 × 280×10^9 = **5.6×10^11 FLOPs/token** — exactly the leak's "560 TFLOPs." **All GPT-4 architecture numbers are unofficial estimates.**

### DeepSeek-V3 — official params, shows MoE efficiency
- "a strong Mixture-of-Experts (MoE) language model with **671B total parameters with 37B activated for each token**"; trained on **14.8T tokens** in only **2.788M H800 GPU hours** — [arXiv:2412.19437](https://arxiv.org/abs/2412.19437) (official).
- **Forward FLOPs/token = 2 × 37×10^9 = 7.4×10^10** — about **11× cheaper per token than Llama 405B** (8.1×10^11 / 7.4×10^10 ≈ 10.9) despite having 1.7× more total parameters. This is the MoE trade: store many parameters, compute with few.
- Training via 6ND: 6 × 37×10^9 × 14.8×10^12 ≈ **3.3×10^24 FLOPs** (our arithmetic on official figures) — ~11× less than Llama 3.1 405B's total.

---

## 3. Comparisons for a general audience (arithmetic shown)

Baseline: **one Llama-405B token = 8.1×10^11 FLOPs**. One year = 365.25 × 86,400 s = **3.156×10^7 seconds**.

### a. One human, one multiplication per second
- 8.1×10^11 FLOPs ÷ 1 FLOP/s = 8.1×10^11 seconds.
- 8.1×10^11 ÷ 3.156×10^7 s/year = **25,666 years ≈ 26,000 years**.
- **One token = one person doing arithmetic nonstop since before the last Ice Age peak.** (For GPT-4's estimated 5.6×10^11: ÷ 3.156×10^7 ≈ 17,700 years.)

### b. Human lifetimes of arithmetic
- One 80-year lifetime of nonstop 1 op/s: 80 × 3.156×10^7 = 2.52×10^9 operations.
- 8.1×10^11 ÷ 2.52×10^9 = **~320 lifetimes per token**.

### c. Cray-1, the 1976 supercomputer
- Cray-1 peak: **160 MFLOPS = 1.6×10^8 FLOP/s**, released 1976 — [Wikipedia: Cray-1](https://en.wikipedia.org/wiki/Cray-1) ("The 160 MFLOPS Cray-1 was succeeded in 1982 by the 800 MFLOPS Cray X-MP").
- Per token: 8.1×10^11 ÷ 1.6×10^8 = 5,062.5 s ÷ 60 = **~84 minutes of the world's fastest 1976 computer for ONE token**. (GPT-4 est.: 5.6×10^11 ÷ 1.6×10^8 = 3,500 s ≈ 58 min. DeepSeek-V3: 7.4×10^10 ÷ 1.6×10^8 ≈ 463 s ≈ 7.7 min.)
- **Training** Llama 3.1 405B on a Cray-1: 3.8×10^25 ÷ 1.6×10^8 = 2.375×10^17 seconds. In years: 2.375×10^17 ÷ 3.156×10^7 = **7.5×10^9 = 7.5 billion years** — more than half the age of the universe (~13.8 billion years, [Wikipedia: Age of the universe](https://en.wikipedia.org/wiki/Age_of_the_universe)). Started at the Big Bang, a Cray-1 would still be only ~55% done... twice over — you could have run the job start-to-finish and be 1 billion years into a second run.

### d. Why it's feasible at all: modern GPUs
- NVIDIA H100 SXM: 1,979 TFLOPS BF16 Tensor Core *with sparsity*, i.e. ≈ **989 TFLOPS ≈ 1×10^15 FLOP/s dense** — [nvidia.com/en-us/data-center/h100](https://www.nvidia.com/en-us/data-center/h100/) (official spec, theoretical peak).
- Per token: 8.1×10^11 ÷ 9.89×10^14 = 8.2×10^-4 s ≈ **0.8 ms of one H100 at peak**. One H100 ≈ 6 million Cray-1s (9.89×10^14 ÷ 1.6×10^8 ≈ 6.2×10^6).
- (Real inference runs below peak utilization and is memory-bandwidth-bound, but the scale is right: what took the 1976 machine 84 minutes takes ~a millisecond today.)

---

## 4. Source ledger: official vs. third-party

| Figure | Value | Type | URL |
|---|---|---|---|
| 2N forward / 6N training per token | formula | Peer-reviewed paper (Kaplan et al. 2020) | https://ar5iv.labs.arxiv.org/html/2001.08361 |
| Attention correction 2·n_layer·n_ctx·d_model | formula | Same paper, Sec. 2.1 | https://ar5iv.labs.arxiv.org/html/2001.08361 |
| 6 × params × tokens methodology; backward:forward ≈ 2:1 | formula | Third-party methodology (Epoch AI) | https://epoch.ai/blog/estimating-training-compute, https://epoch.ai/blog/backward-forward-FLOP-ratio |
| Llama 3.1 405B: 405B params, 15.6T tokens, 3.8×10^25 FLOPs, 126 layers, d_model 16,384 | official | Meta paper | https://arxiv.org/abs/2407.21783 |
| Llama 3.1 405B compute (corroboration) | 3.8e25 | Third-party (Epoch AI) | https://epoch.ai/data-insights/models-over-1e25-flop |
| GPT-4 training compute ~2×10^25 (2.1e25) | estimate | Third-party (Epoch AI) | https://epoch.ai/data-insights/models-over-1e25-flop |
| GPT-4 1.8T total / ~280B active / 560 TFLOPs per token | unofficial leak | Third-party (SemiAnalysis, paywalled; secondary summaries) | https://www.semianalysis.com/p/gpt-4-architecture-infrastructure, https://the-decoder.com/gpt-4-architecture-datasets-costs-and-more-leaked/, https://patmcguinness.substack.com/p/gpt-4-details-revealed |
| DeepSeek-V3: 671B/37B active, 14.8T tokens, 2.788M H800 GPU-hours | official | DeepSeek paper | https://arxiv.org/abs/2412.19437 |
| Cray-1: 160 MFLOPS peak, 1976 | reference | Wikipedia | https://en.wikipedia.org/wiki/Cray-1 |
| H100 SXM: 1,979 TFLOPS BF16 (sparsity) ≈ 989 dense | official spec | NVIDIA | https://www.nvidia.com/en-us/data-center/h100/ |
| Age of universe ~13.8 Gyr | reference | Wikipedia | https://en.wikipedia.org/wiki/Age_of_the_universe |

**Presentation one-liner:** Every single token Llama-405B emits costs ~810 billion floating-point operations — 84 minutes on the fastest computer of 1976, or one human doing arithmetic nonstop for 26,000 years — and your GPU does it in under a millisecond.
