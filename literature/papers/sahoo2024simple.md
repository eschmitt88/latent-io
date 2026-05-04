---
kind: paper
title: "Simple and Effective Masked Diffusion Language Models (MDLM)"
authors: ["Subham Sekhar Sahoo", "Marianne Arriola", "Yair Schiff", "Aaron Gokaslan", "Edgar Marroquin", "Justin T Chiu", "Alexander Rush", "Volodymyr Kuleshov"]
year: 2024
venue: "NeurIPS 2024 (Cornell Tech)"
url: "https://arxiv.org/abs/2406.07524"
source: "raw/papers/sahoo2024simple.pdf"
added: "2026-05-04"
relevance: 3
status: skimmed
related_experiments: []
related_concepts: []
tags: ["foundational", "masked-diffusion", "rao-blackwell", "training-recipe"]
---

# MDLM: Simple and Effective Masked Diffusion LMs

## TL;DR

Masked discrete diffusion is more performant than previously thought. A modern training recipe plus a Rao-Blackwellized objective — provably a sharper estimator — yields a state-of-the-art among diffusion LMs that approaches AR perplexity. The objective reduces to a simple mixture of classical masked-LM losses, so it's a drop-in replacement for the standard MLM training recipe.

## Claims

- The performance gap between diffusion and AR LMs reported in earlier work is largely an artifact of suboptimal training recipes, not a fundamental limitation of diffusion.
- Rao-Blackwellizing the masked diffusion objective reduces variance and improves performance — and simplifies the loss to a mixture of masked LM losses.
- The same model admits both parallel sampling and semi-autoregressive sampling that generates arbitrary lengths.

## Methods

- Standard encoder-only transformer trained with a Rao-Blackwellized masked-diffusion objective.
- Modern training recipe: better loss weighting, schedules, sampling.

## Results

- SOTA among diffusion LMs at matched scale.
- Approaches AR perplexity on language modeling benchmarks.
- Efficient sampling — both parallel and semi-AR.

## Critique / open questions

- "Approaches AR" is not "matches AR"; the gap is real but smaller than prior work suggested.
- Rao-Blackwellization is a variance reduction; whether it changes the fundamental scaling behavior at very large scale is unstudied.

## Follow-up

**Relevance:** 3 — foundational training recipe. The cleanest baseline for any project experiment that needs a small trainable diffusion LM. Code at github.com/kuleshov-group/mdlm.
