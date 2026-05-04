---
kind: paper
title: "ReFusion: A Diffusion Large Language Model with Parallel Autoregressive Decoding"
authors: ["Jia-Nan Li", "Jian Guan", "Wei Wu", "Chongxuan Li"]
year: 2026
venue: "ICLR 2026 (RUC, Ant Group, Ant International)"
url: "https://arxiv.org/abs/2512.13586"
source: "raw/papers/li2026refusion.pdf"
added: "2026-05-04"
relevance: 4
status: skimmed
related_experiments: []
related_concepts: ["commitment-boundary"]
tags: ["diffusion-lm", "kv-cache", "slot-level-decoding", "hybrid", "iclr-2026"]
---

# ReFusion: Diffusion + Parallel AR Decoding

## TL;DR

Hybrid that elevates parallel decoding from the token level to a *slot* level: each iteration does (1) a diffusion-based selection of which weakly-dependent slots to decode next, (2) intra-slot autoregressive infilling. This unlocks full KV-cache reuse (which pure MDM precludes) while preserving diffusion's parallelism. 34% gain over prior MDMs, 18× speedup, 2.33× speedup over strong AR baselines.

## Claims

- Pure masked-diffusion suffers from two structural costs: no KV-cache reuse and incoherent generation from learning over an intractable space of token combinations.
- Both fall away if you do diffusion at the *slot* level (groups of tokens) and AR within each slot.
- The slot-level structure also gives a learning-complexity reduction: dependencies are easier to model among slots than among arbitrary token combinations.

## Methods

- Sequence partitioned into fixed-length consecutive slots.
- Per iteration: diffusion plans which slots to decode, AR fills each selected slot, decoded slots get reordered ahead of the remaining masks.
- Standard transformer with causal attention adapted to handle reorganization.

## Results

- 34% perf gain over prior MDMs.
- 18× speedup vs. MDMs; 2.33× vs. AR baselines.
- KV cache fully reusable (unlike LLaDA / pure MDM).

## Critique / open questions

- Slot size is a hyperparameter; the paper picks one but the sensitivity isn't deeply analyzed.
- AR-within-slot reintroduces local commitment; the design is a hybrid, not a pure non-AR architecture.

## Follow-up

**Relevance:** 4 — the most explicit attempt to navigate the AR↔diffusion design space. Directly relevant to the project's question of *where the right commitment granularity sits* — ReFusion picks slots; the project might pick something different. Code at github.com/ML-GSAI/ReFusion. Model at huggingface.co/GSAI-ML/ReFusion.
