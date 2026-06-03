---
kind: paper
title: "CODI: Compressing Chain-of-Thought into Continuous Space via Self-Distillation"
authors: ["Zhenyi Shen", "Hanqi Yan", "Linhai Zhang", "Zhanghao Hu", "Yali Du", "Yulan He"]
institutions: ["King's College London", "The Alan Turing Institute"]
year: 2025
venue: "EMNLP 2025 (KCL, Alan Turing Institute)"
peer_reviewed: true
url: "https://aclanthology.org/2025.emnlp-main.36/"
code_url: "https://github.com/zhenyi4/codi"
citations: null
source: "raw/papers/shen2025codi.pdf"
added: "2026-05-04"
relevance: 3
credibility: 4
status: skimmed
related_experiments: []
related_concepts: ["continuous-thought"]
tags: ["self-distillation", "implicit-cot", "no-teacher", "emnlp-2025"]
---

# CODI: Compressing CoT into Continuous Space via Self-Distillation

## TL;DR

Self-distillation framework that jointly trains a teacher task (explicit text CoT) and a student task (implicit continuous CoT) on the same model — distilling the reasoning into continuous space without a separately trained teacher. Closes much of the gap between implicit-CoT and explicit-CoT methods that prior implicit approaches couldn't.

## Claims

- Prior implicit-CoT methods consistently underperform explicit CoT — the gap is not fundamental but training-signal-driven.
- A model can teach itself: the same weights produce both an explicit CoT (reasoning trace + answer) and an implicit CoT (continuous thoughts + answer); the latter is supervised against the former.
- Self-distillation removes the dependence on a stronger teacher model — the same architecture handles both modes.

## Methods

- Joint training: half the batches go through "teacher mode" (explicit CoT, normal LM loss), half through "student mode" (implicit continuous CoT, distillation loss against teacher hidden states).
- Inference uses student mode (cheap, fast).

## Results

- Closes most of the implicit-vs-explicit gap on standard reasoning benchmarks.
- No external teacher needed.

## Critique / open questions

- Joint training is more delicate than two separate trainings; balancing teacher/student losses isn't trivial.
- Whether the student converges to genuinely "implicit" reasoning vs. "compressed surface CoT" is an open empirical question — the distinction matters for whether the latent thoughts encode something tokens can't.

## Trust signals

- **Credibility:** 4 — KCL + Alan Turing Institute; EMNLP 2025 peer-reviewed; official code released (zhenyi4/codi).

## Follow-up

**Relevance:** 3 — methodologically attractive (no separate teacher) and directly useful if the project wants to bootstrap latent reasoning on top of an existing CoT-trained base model rather than train from scratch.
