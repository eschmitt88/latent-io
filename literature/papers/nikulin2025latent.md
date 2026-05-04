---
kind: paper
title: "Latent Action Learning Requires Supervision in the Presence of Distractors (LAOM)"
authors: ["Alexander Nikulin", "Ilya Zisman", "Denis Tarasov", "Nikita Lyubaykin", "Andrei Polubarov", "Igor Kiselev", "Vladislav Kurenkov"]
year: 2025
venue: "ICML 2025 (dunnolab)"
url: "https://arxiv.org/abs/2502.00379"
source: "raw/papers/nikulin2025latent.pdf"
added: "2026-05-04"
relevance: 4
status: skimmed
related_experiments: []
related_concepts: ["action-observation-trace"]
tags: ["latent-action", "supervision", "distractors", "negative-finding", "icml-2025"]
---

# LAOM: Latent Action Learning Requires Supervision

## TL;DR

Pure unsupervised latent-action learning (à la LAPO) fails when observation streams contain action-correlated distractors — real-world videos always have them. Proposed LAOM: drop codebook quantization for high-capacity continuous latents, use multi-step inverse dynamics (not single-step), latent-space forward dynamics, and augmentations. Result: 8× quality improvement (linear-probe metric); adding 2.5% ground-truth action labels gives 4.2× downstream improvement on top of that.

## Claims

- Real-world video doesn't satisfy the assumption that frame-to-frame change is dominated by agent action — distractors (other agents, scene change, lighting) confound LAM training.
- Several modifications individually help: continuous (not quantized) latents, multi-step inverse dynamics, latent-space forward dynamics, augmentations. Together they give 8× quality.
- A small amount of ground-truth supervision (2.5%) buys outsized gains (4.2×) — fully unsupervised LAM training is suboptimal in practice.

## Methods

- Distracting Control Suite (DCS) as the benchmark for evaluating LAM under distractor noise.
- LAOM modifications stacked onto LAPO base.
- Linear probing of latent actions against ground-truth actions to measure latent quality.

## Results

- 8× linear-probe latent action quality improvement vs. LAPO.
- 4.2× downstream task performance improvement when 2.5% of labels are added during latent learning.

## Critique / open questions

- Distracting Control Suite is synthetic; real-world video distractors have different structure.
- "2.5% labels" is a small but non-zero overhead; whether even smaller fractions suffice is unstudied.

## Follow-up

**Relevance:** 4 — important *negative finding* for the project's training-signal open question (NOTES.md #4). Pure unsupervised latent learning underperforms when realistic noise is present; hybrid supervised/self-supervised is the practical path. This directly informs how to design training for project experiments — a small budget of labeled data is essential.
