---
url: https://dentro.de/ai/visualizations/, https://tiktokenizer.vercel.app/, https://poloclub.github.io/transformer-explainer/, https://bbycroft.net/llm, https://animatedllm.github.io/, https://playground.tensorflow.org/, https://projector.tensorflow.org/
fetched: 2026-08-12
---

# Demo Embeddability Probe (iframe from another origin)

**Method:** `curl -sIL <url>` (HEAD, follow redirects), then re-verified with GET (`curl -sL -D - -o /dev/null`) since some CDNs attach CSP only on GET. Recorded HTTP status, `X-Frame-Options` (XFO), and `Content-Security-Policy: frame-ancestors`. Rule: no XFO and no `frame-ancestors` → embeddable cross-origin.

**Caveat:** header absence is necessary but not strictly sufficient — a page can still frame-bust in JavaScript (`if (top !== self) ...`). None of these are known to, but do a 5-minute live test in the actual deck before presenting.

## Verdict table

| Demo | URL | Status | X-Frame-Options | CSP frame-ancestors | Verdict |
|---|---|---|---|---|---|
| Transformer Explainer (Polo Club) | https://poloclub.github.io/transformer-explainer/ | 200 | — | — | **EMBEDDABLE** |
| LLM Visualization (Brendan Bycroft) | https://bbycroft.net/llm | 200 | — | — | **EMBEDDABLE** |
| Animated LLM | https://animatedllm.github.io/ | 200 | — | — | **EMBEDDABLE** |
| Tiktokenizer | https://tiktokenizer.vercel.app/ | 200 | — | — | **EMBEDDABLE** |
| dentro.de visualization collection | https://dentro.de/ai/visualizations/ (301 → trailing slash) | 301→200 | — | — | **EMBEDDABLE** |
| TensorFlow Playground | https://playground.tensorflow.org/ | 200 | — | — | **EMBEDDABLE** |
| Embedding Projector | https://projector.tensorflow.org/ | 200 | — | — | **EMBEDDABLE** |
| Moebio Mind | https://moebio.com/mind/ | 200 | — | — | **EMBEDDABLE** |
| Raschka: Big LLM Architecture Comparison | https://magazine.sebastianraschka.com/p/the-big-llm-architecture-comparison | 200 | — | `'self' https://*.substack.com https://substack.com` | **MUST OPEN IN NEW TAB** |
| BertViz (Colab notebook) | https://colab.research.google.com/drive/1hXIQ77A4TYS4y3UthWF-Ci7V7vVUoxmQ | 200 | `DENY` | — | **MUST OPEN IN NEW TAB** |
| YouTube watch page (any video) | https://www.youtube.com/watch?v=LPZh9BOjkQs | 200 | `SAMEORIGIN` | — | **MUST OPEN IN NEW TAB** (watch URL) |
| YouTube embed endpoint | https://www.youtube.com/embed/LPZh9BOjkQs | 200 | — | — | **EMBEDDABLE** (use `/embed/<id>`, not `/watch`) |

Bottom line: **every core demo for the deck is iframe-embeddable.** Only Substack, Colab, and YouTube `/watch` pages block framing — and YouTube has the standard `/embed/` workaround.

## Tiktokenizer canonical URL

Canonical URL confirmed as **https://tiktokenizer.vercel.app/** — it is the deployment of the open-source project [dqbd/tiktokenizer](https://github.com/dqbd/tiktokenizer) ("Online playground for OpenAI tokenizers"), and it is the URL the dentro.de collection itself links (with a useful deep-link parameter: `https://tiktokenizer.vercel.app/?model=cl100k_base` — the `model` query param preselects a tokenizer, handy for a live demo).

## What dentro.de/ai/visualizations curates

Fetched 2026-08-12. It is a small, high-signal curated list in three sections:

**Interactive websites**
1. **Tiktokenizer** — https://tiktokenizer.vercel.app/?model=cl100k_base — tokenization: how LLMs split text into tokens (already in our list).
2. **Moebio Mind** — https://moebio.com/mind/ — interactive neural-network visualization of interconnected nodes.
3. **Transformer Explainer** — https://poloclub.github.io/transformer-explainer/ — self-attention inside a live GPT-2 (already in our list).
4. **BertViz** — https://colab.research.google.com/drive/1hXIQ77A4TYS4y3UthWF-Ci7V7vVUoxmQ — head-by-head self-attention visualization for BERT-family transformers (Colab notebook).
5. **LLM Visualization** — https://bbycroft.net/llm — 3D walkthrough of the full LLM pipeline, tokenization → prediction (already in our list).
6. **The Big LLM Architecture Comparison** (Sebastian Raschka) — https://magazine.sebastianraschka.com/p/the-big-llm-architecture-comparison — side-by-side architecture diagrams of Llama/Mistral/DeepSeek etc.

**Videos**
7. **"Large Language Models Explained Briefly"** (3Blue1Brown) — https://www.youtube.com/watch?v=LPZh9BOjkQs — 8-minute visual overview of next-word prediction.
8. **"Deep Dive into LLMs like ChatGPT"** (Andrej Karpathy) — https://www.youtube.com/watch?v=7xTGNNLPyMI — full training pipeline: pretraining, fine-tuning, RLHF.

**Fun challenges**
9. **Bouncing Ball in Hexagon** — https://x.com/flavioAd/status/1885449107436679394 — informal physics-sim coding benchmark across models.
10. **Vitruvian Robot** — https://nitter.poast.org/renntv/status/1958854737761304895 — SVG generation compared across 37+ models.

## Most presentation-worthy additions from the collection (probed above)

1. **Moebio Mind** (https://moebio.com/mind/) — embeddable; an artistic network-of-nodes visual, good as a mood-setting opener for the neural-network history act.
2. **BertViz** (Colab link above) — the classic attention-heads visualization; Colab blocks iframes (XFO: DENY), so open in new tab or screen-record a GIF beforehand.
3. **3Blue1Brown "LLMs Explained Briefly"** — embed via https://www.youtube.com/embed/LPZh9BOjkQs; best available animation of next-token prediction and scale for a general audience.
4. **Raschka's Big LLM Architecture Comparison** — new-tab only (Substack CSP); its architecture diagrams are the clearest "what changed between Llama/Mistral/DeepSeek" visuals available.
5. **Karpathy "Deep Dive into LLMs"** — embed via https://www.youtube.com/embed/7xTGNNLPyMI; useful clip source for the training-pipeline segment.

Note: the collection has nothing dedicated to embeddings — for that topic use **https://projector.tensorflow.org/** (probed above, embeddable), which pairs with **https://playground.tensorflow.org/** for the history act (both are classic Google demos, both frame-friendly).
