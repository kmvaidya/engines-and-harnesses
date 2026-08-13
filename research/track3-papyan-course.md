---
url: https://sites.google.com/view/mat1510 ; https://sites.google.com/view/vardan-papyan/home
fetched: 2026-08-12
---

# Track 3 — Vardan Papyan's UofT Deep Learning Course (MAT1510)

**Status: FOUND.** The Google Sites course page exists and is public:

- **Course site (main / current = Fall 2025):** https://sites.google.com/view/mat1510
- Year subpages: https://sites.google.com/view/mat1510/fall-2025 | https://sites.google.com/view/mat1510/fall-2024 | https://sites.google.com/view/mat1510/fall-2023 | https://sites.google.com/view/mat1510/fall-2022 | https://sites.google.com/view/mat1510/winter-2021
- **Instructor homepage:** https://sites.google.com/view/vardan-papyan/home (also resolves from https://sites.google.com/view/vardan-papyan)
- UofT math directory entry: https://www.mathematics.utoronto.ca/people/directories/all-faculty/vardan-papyan
- Contact listed on site: vardan.papyan@utoronto.ca

**Course:** MAT1510 — *Deep Learning: Theory & Data Science*, University of Toronto, Department of Mathematics (Papyan is Associate Professor, Math + CS cross-appointment; Vector Institute faculty; Schwartz Reisman affiliate; postdoc under David Donoho at Stanford; PhD under Michael Elad at Technion).

**Important correction to the brief:** this is a *graduate theory-of-deep-learning* course, not an intro "MLPs → CNNs → RNNs → transformers" survey. The site is exactly as reported a Google Sites page dense with lecture-slide links (Google Drive PDFs) — but it does **not** link classic interactive demos (no TensorFlow Playground, no CNN Explainer, no LSTMVis). Verified by grepping the raw HTML of all five year-pages for external hrefs. The nearest things to "interactive demos" it links are Anthropic's interactive-figure article *Toy Models of Superposition* and Colab notebooks (details below).

---

## 1. Course structure / syllabus arc

### Fall 2025 (current version, on the landing page)

Course description (verbatim): *"Deep learning systems have revolutionized field after another, leading to unprecedented empirical performance. Yet, their intricate structure led most practitioners and researchers to regard them as blackboxes, with little that could be understood. In this course, we will review experimental and theoretical works aiming to improve our understanding of modern deep learning systems."*

Evaluation: 20% attendance/participation, 40% "tiny PyTorch coding exercises," 40% final project (pick a paper, 2-page report = 1 page summary + 1 page novel theoretical result or novel experiment, 5-min talk).

Lecture arc, in page order (section headers are his):

**Background**
1. What Is This Course About?
2. Introduction to Deep Learning
3. Transformers

**Theories on Architectures**
4. Transformers as Dynamical Systems

**Theories on Optimization**
5. Optimization + Parameter Efficient Fine-Tuning (LoRA)
6. Implicit Bias of Gradient Descent on Separable Data
7. Other Implicit Biases

**Theories on Representations**
8. Information Bottleneck
9. Neural Collapse + Unconstrained Features Model
10. Toy Models of Superposition
11. Grokking

**Theories on Infinite-Width**
12. Neural Network Gaussian Processes
13. Neural Tangent Kernel
14. Generalization Through NTK Dynamics
15. Lazy vs. Active Learning
16. Mean-Field Theory

**Theories of LLMs**
17. Scaling Laws
18. From Scaling to Capabilities (emergence, chain-of-thought)
19. In-Context Learning

**Theories of Diffusion Models**
20. Introduction to Diffusion Models
21. Generalization in Diffusion Models

**Safety and Alignment**
22. Jailbreaking

### How the syllabus evolved year-to-year (useful as a mini-history in itself)

- **Winter 2021:** canonical datasets, optimization, sparsity & information compression, "Failure of Theory," adversarial examples, logistic regression → max-margin implicit bias, discriminant analysis → **Neural Collapse block (5 lectures)**, random matrix theory / deep-net Hessian spectra, kernels → NNGP → NTK, lazy vs. active training, multilayered convolutional sparse coding. No transformers at all.
- **Fall 2022:** mysteries in DL, information bottleneck + its criticism, rethinking generalization, max-margin implicit bias, Neural Collapse, NNGP/NTK, Hessian spectrum at scale, random matrix theory, mean-field. Still no transformers.
- **Fall 2023:** **Transformers lecture first appears** (plus batch normalization); otherwise theory core intact.
- **Fall 2024:** adds **Chain of Thought, LoRA, Security & Safety in AI, Diffusion Models**.
- **Fall 2025:** adds whole sections — **Theories of LLMs (scaling laws, emergence, in-context learning), Toy Models of Superposition, Grokking, Transformers as Dynamical Systems, Jailbreaking**.

The drift 2021→2025 (sparse coding & RMT out; transformers, scaling laws, superposition, grokking, jailbreaking in) is a compact live record of where the field's center of gravity moved.

---

## 2. Interactive demos / interactive-adjacent links on the site

Checked exhaustively (raw-HTML grep of all five year pages). **No TensorFlow Playground, CNN Explainer, LSTMVis, distill.pub, or transformer-visualizer links exist on the site.** What it does link:

- **Toy Models of Superposition** (Anthropic transformer-circuits, interactive figures): https://transformer-circuits.pub/2022/toy_model/index.html
- **Anthropic research index** (linked from safety/alignment and project-topic suggestions): https://www.anthropic.com/research (Fall 2024 variant links https://www.anthropic.com/research#overview)
- **Colab coding exercises** (hands-on PyTorch, Fall 2025): HW1 https://colab.research.google.com/drive/1KSesfne2jKbC-w2X5IUz1NwdIebPtK9D?usp=sharing · HW2 https://colab.research.google.com/drive/13owvv1lBN6PEMlUFneykG7GHlA_iqAJe?usp=sharing · HW3 https://colab.research.google.com/drive/11oXRTu1W_WiMvtjS0Fc9ymh1hp_IKkYn?usp=sharing · HW4 https://colab.research.google.com/drive/1yiG5O0LT4kxro33RipYfMjHReasue2MZ?usp=sharing (Winter 2021/Fall 2022 pages have up to HW9-length Colab sequences)
- **Course "Music": "I'm Your GPU"** — a novelty song linked right on the syllabus: https://www.youtube.com/watch?v=C9_ooljYl60 (fun opener/closer material)

---

## 3. Framing worth borrowing for a history-of-neural-networks act

- **The "blackbox" framing:** his one-paragraph course description is a ready-made thesis line — deep nets revolutionized "field after another" *before* we understood them; the course (and arguably the last decade of theory) is the attempt to catch up. Good pivot from "history of what we built" to "history of what we understand."
- **Syllabus-as-timeline:** the five year-pages (2021→2025) physically document the field's shift — sparse coding/RMT era → generalization mysteries → transformers → LLM science (scaling laws, emergence, in-context learning) → safety/jailbreaking. You can screenshot the five syllabi side by side.
- **Neural Collapse as "a law found in the wild":** his own discovery (with X.Y. Han and David Donoho, PNAS 2020, https://arxiv.org/abs/2008.08186) is a core lecture every single year — the observation that in late training, last-layer class means collapse to a simplex equiangular tight frame. It's a rare example of a crisp, universal empirical regularity in deep nets — a good "modern physics-style discovery" beat. Course pairs it with the Unconstrained Features Model (https://arxiv.org/pdf/2011.11619).
- **Motivating attention/transformers:** he does NOT do the classic "RNNs are limited → attention" arc; transformers enter via *Attention Is All You Need* (https://arxiv.org/abs/1706.03762) and then get treated *mathematically* — "Transformers as Dynamical Systems": tokens as interacting particles that **cluster** as they flow through depth (https://arxiv.org/abs/2305.05465, https://arxiv.org/pdf/2312.10794 — "A mathematical perspective on Transformers"). That's a distinctive, visual, and borrowable framing (particle-clustering animations exist in those papers).
- **Mysteries genre:** the recurring "Mysteries in Deep Learning" / "Rethinking Generalization" lecture (Zhang et al.'s nets-memorize-random-labels result) is the standard hook for why classical learning theory broke ~2017.
- **Textbook anchors:** Arora et al., *Theory of Deep Learning* draft: https://www.cs.princeton.edu/~arora/TheoryDL.pdf ; Roberts/Yaida, *The Principles of Deep Learning Theory*: https://arxiv.org/pdf/2106.10165

---

## 4. Public slide decks (Google Drive, all publicly linked from the site)

### Fall 2025 slides
| Lecture | URL |
|---|---|
| What Is This Course About? | https://drive.google.com/file/d/16ab_OqW-uor1KZFRTOu1nF6LojlHxJK5/view?usp=sharing |
| Introduction to Deep Learning | https://drive.google.com/file/d/1lM914Lf05VqmqKBsSmZlk3d2Gedzd-_o/view?usp=sharing |
| Transformers | https://drive.google.com/file/d/1nO6B2pbvqUyks3hR1Dwj1HWpgiWVP0tH/view?usp=sharing |
| Transformers as Dynamical Systems | https://drive.google.com/file/d/1MXzisv3U_pkjxzSmC-l3sfyB0pB0i97R/view?usp=sharing |
| Optimization | https://drive.google.com/file/d/1WuWXfR5w2LHNi6Lv_uqr2JABxwFEg96U/view?usp=sharing |
| Parameter Efficient Fine-Tuning | https://drive.google.com/file/d/1PNFQDMo5DWWmIXsOaroq8DZi6wYQ8lQi/view?usp=sharing |
| Implicit Bias of Gradient Descent | https://drive.google.com/file/d/1a4T2W4dynlsXS8kqLIaEytsbAs9d5Vac/view?usp=sharing |
| Other Implicit Biases | https://drive.google.com/file/d/1QNN3E1m62rp0Ib6qoaYPyGvKNTeSMZ0-/view?usp=sharing |
| Information Bottleneck | https://drive.google.com/file/d/1Dv5opgJJOHJJQ7APXOxMvu8qXdaWPSm-/view?usp=sharing |
| Neural Collapse | https://drive.google.com/file/d/1laYTdHA1ch20IOpEPSRKzaipraUPm_fE/view?usp=sharing |
| Unconstrained Features Model | https://drive.google.com/file/d/1tTfQ_8gs6b5pG-8fPCZM459FZ26RvuI0/view?usp=sharing |
| Toy Models of Superposition | https://drive.google.com/file/d/1fUuwZOAlDiVAiLXMMibEn8MrdxOPPk0l/view?usp=sharing |
| Neural Network Gaussian Processes | https://drive.google.com/file/d/1HrJJ2MmS25TdMLGobNBk8n_48cKvkwP6/view?usp=sharing |
| Neural Tangent Kernel | https://drive.google.com/file/d/1DnbNcWDPzEFn5s5ZfVpfl_IiihTdPT6T/view?usp=sharing |
| Lazy vs. Active Learning | https://drive.google.com/file/d/1x2xZ2eMrsxevqX_cYjtSX_REgJdjcLvS/view?usp=sharing |

(Remaining Fall 2025 topics — Grokking, Generalization Through NTK, Mean-Field, Scaling Laws, From Scaling to Capabilities, In-Context Learning, Diffusion, Jailbreaking — are linked as "(paper)" arxiv references rather than slide PDFs on the current page.)

### Winter 2021 slides (28 per-topic PDFs — includes the most "history-friendly" intro decks)
Selected (full list on https://sites.google.com/view/mat1510/winter-2021):
- What Is This Course About? — https://drive.google.com/file/d/1QXwlw3iPMhZy8YfXnvcnv677JUfvbHJb/view?usp=sharing
- Canonical datasets — https://drive.google.com/file/d/1xr54X-5WhS2x0lJz8cFqY2X63Jw2RD0f/view?usp=sharing
- Optimization — https://drive.google.com/file/d/1rxdvi6cBmYd2xjEqRwCZOywpybeMB8Df/view?usp=sharing
- Adversarial Examples — https://drive.google.com/file/d/1ng5SxcT9-J82PzOxJWNceMN-8LXpbrdT/view?usp=sharing
- Neural Collapse: Empirical Evidence — https://drive.google.com/file/d/1GxmGQMNrrZQwvlZUMwNUBD_sUwQnwnIt/view?usp=sharing
- Neural Collapse: Optimality — https://drive.google.com/file/d/1ZWqt4iywNNGhPtF4XQo_fK2FIKG-zRy-/view?usp=sharing
- Introduction to Random Matrix Theory — https://drive.google.com/file/d/1q0sxATG4qgIoFwJfukPuHW7DL6ZPeDlA/view?usp=sharing
- Neural Network Gaussian Processes — https://drive.google.com/file/d/1oQFE4K064i-ePe5Cx3ypgQukBYU57-_5/view?usp=sharing
- Neural Tangent Kernel — https://drive.google.com/file/d/1AocXSSv4y1SCQwdXtt_NqgxFUUJDCMTt/view?usp=sharing
- Multilayered Convolutional Sparse Coding — https://drive.google.com/file/d/1N69HkFhjo3LvV-906Yw2y4bqZRcSOgbz/view?usp=sharing

### Winter 2021 recorded lectures (full YouTube run, Lectures 3–24)
https://youtu.be/63F6xgFxll0 · https://youtu.be/fmH3sDe34dE · https://youtu.be/MkrNasMqhvA · https://youtu.be/lUpfOECIHoM · https://youtu.be/b4xEsN8NeYI · https://youtu.be/g8XPYoh0wXw · https://youtu.be/ptDEXGVX-QQ · https://youtu.be/H4QBckbY_Hg · https://youtu.be/VnhsWca7bcE · https://youtu.be/FIH1JJWK4kY · https://youtu.be/tXJBlG7rAVk · https://youtu.be/4q54WYByaBU · https://youtu.be/-cMjm6i71DM · https://youtu.be/VsWLcJo1OcI · https://youtu.be/vj9mNWPdBVo · https://youtu.be/Er_lUzkZsMg · https://youtu.be/_aSB2ElEg6g · https://youtu.be/oMkpIqU8djc · https://youtu.be/Hry16Ba0TkU · https://youtu.be/V-N0RK1uGKo · https://youtu.be/kQWz4Ir0c6k · https://youtu.be/8uFY54g8alw

### Key papers the Fall 2025 page attaches to each lecture (selection)
- Transformers: https://arxiv.org/abs/1706.03762 · Dynamical systems view: https://arxiv.org/abs/2305.05465, https://arxiv.org/pdf/2312.10794
- Adam: https://arxiv.org/abs/1412.6980 · LoRA: https://arxiv.org/abs/2106.09685
- Implicit bias: https://arxiv.org/abs/1710.10345, https://arxiv.org/abs/1906.05890, https://arxiv.org/abs/1705.09280, https://arxiv.org/abs/1905.13655, https://arxiv.org/abs/1810.02032, https://arxiv.org/abs/2404.04454
- Information Bottleneck: https://arxiv.org/abs/1503.02406 · Neural Collapse: https://arxiv.org/abs/2008.08186 + https://arxiv.org/pdf/2011.11619 · Grokking: https://arxiv.org/abs/2201.02177
- NNGP: https://arxiv.org/abs/1711.00165 · NTK: https://arxiv.org/abs/1806.07572 · NTK generalization: https://arxiv.org/abs/1901.08584 · Lazy training: https://arxiv.org/abs/1812.07956 · Mean-field: https://arxiv.org/abs/1804.06561
- Scaling laws: https://arxiv.org/abs/1712.00409, https://arxiv.org/abs/2001.08361, https://arxiv.org/abs/2203.15556 (Chinchilla) · Capabilities/emergence/CoT: https://arxiv.org/abs/2005.14165 (GPT-3), https://arxiv.org/abs/2206.07682, https://arxiv.org/abs/2201.11903, https://arxiv.org/abs/2205.11916
- Diffusion: https://arxiv.org/pdf/2006.11239 (DDPM), https://arxiv.org/abs/2310.02557 · Jailbreaking: https://arxiv.org/abs/2307.15043 (GCG universal adversarial suffixes)
- Also linked: https://arxiv.org/abs/2406.04267 (information squashing in transformers)

---

## 5. His research as it appears in the course framing

- **Neural Collapse** (Papyan, Han, Donoho — *Prevalence of neural collapse during the terminal phase of deep learning training*, PNAS 2020; arXiv: https://arxiv.org/abs/2008.08186) is a named lecture in **every** offering 2021–2025; the Winter 2021 offering devoted ~5 lectures to it (empirical evidence → optimality → relation to max-margin/discriminant analysis → unconstrained features model → related works). Follow-up with Han & Donoho on NC under MSE loss won an **ICLR 2022 Outstanding Paper Award** (noted on his homepage, which also lists a "Linguistic Collapse" project — NC in language models).
- His earlier line (Technion, with Elad) — **multilayered convolutional sparse coding** — appears only in the Winter 2021 syllabus and was dropped afterward; itself a small case study of the field moving on.
- The deep-net **Hessian spectrum / random matrix theory** lectures (2021–2022) also trace directly to his Stanford postdoc work with Donoho on measuring deep-net spectra at scale.

## What was NOT found (stated plainly)
- No interactive-demo links (TensorFlow Playground, CNN Explainer, LSTMVis, distill.pub, transformer visualizers) anywhere on any MAT1510 year page — confirmed against raw HTML, not just rendered summaries. If the brief's "interactive demos" memory refers to a Papyan course, it is not on this site; his only other current teaching found is MAT188 Linear Algebra (no public demo-laden course site located).
- No standard intro arc (MLP → CNN → RNN → attention): the course is graduate theory; CNNs/RNNs are not standalone lectures in any year.
- No GitHub course repo found; materials live entirely on Google Sites + Google Drive + Colab + YouTube.
