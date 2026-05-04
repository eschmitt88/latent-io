---
kind: paper
title: "System-1.5 Reasoning: Traversal in Language and Latent Spaces with Dynamic Shortcuts"
authors: ["Xiaoqiang Wang", "Suyuchen Wang", "Yun Zhu", "Bang Liu"]
year: 2025
venue: "NeurIPS 2025 (Mila / U. Montréal)"
url: "https://arxiv.org/abs/2505.18962"
source: "raw/papers/wang2025system.pdf"
added: "2026-05-04"
relevance: 3
status: skimmed
related_experiments: []
related_concepts: ["continuous-thought", "uncertainty-trigger"]
tags: ["latent-reasoning", "shortcuts", "self-distillation", "efficiency"]
---

# System-1.5 Reasoning: Dynamic Shortcuts

## TL;DR

Adaptive reasoning framework that distills text CoT into latent continuous thought, then distills that into two kinds of dynamic shortcuts: a *depth shortcut* (early-exit non-critical tokens through lightweight adapter branches) and a *step shortcut* (reuse hidden states across decoding steps to skip trivial reasoning steps). 20× inference speedup, 91% token reduction on GSM8K, comparable accuracy to text CoT.

## Claims

- Latent reasoning methods that treat all steps uniformly (Coconut, etc.) are inefficient — most steps are auxiliary and don't need full-depth compute.
- Two complementary shortcuts: vertical (depth) and horizontal (step) — the model learns which steps deserve which.
- Two-stage self-distillation: text CoT → latent thought → adaptive shortcuts. Each stage is supervised by the previous.

## Methods

- Stage 1: distill explicit text CoT into continuous thoughts à la Coconut.
- Stage 2: distill the dense latent reasoning into two shortcut paths — depth shortcut (per-token early exit) and step shortcut (hidden-state reuse).
- GSM8K and similar benchmarks.

## Results

- 20× faster inference vs. text CoT, 91% token reduction.
- Comparable accuracy to text CoT — i.e. shortcuts don't lose performance.

## Critique / open questions

- Two-stage distillation requires a well-trained text-CoT teacher to start; doesn't bootstrap from scratch.
- The shortcut policy is learned per-token implicitly — interpretability of "why this step got the shortcut" is opaque.

## Follow-up

**Relevance:** 3 — practical exemplar of "compute belongs where the cognition is dense." The dynamic shortcut policy is essentially an `uncertainty-trigger` over compute (rather than over retrieval) — an interesting parallel that may unify under a single concept.
