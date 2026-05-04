---
kind: paper
title: "Scaling up Test-Time Compute with Latent Reasoning: A Recurrent Depth Approach"
authors: ["Jonas Geiping", "Sean McLeish", "Neel Jain", "John Kirchenbauer", "Siddharth Singh", "Brian R. Bartoldson", "Bhavya Kailkhura", "Abhinav Bhatele", "Tom Goldstein"]
year: 2025
venue: "NeurIPS 2025 spotlight"
url: "https://arxiv.org/abs/2502.05171"
source: "raw/papers/geiping2025scaling.pdf"
added: "2026-05-04"
relevance: 5
status: skimmed
related_experiments: []
related_concepts: ["continuous-thought", "commitment-boundary"]
tags: ["recurrent-depth", "test-time-compute", "no-cot-supervision", "huginn"]
---

# Scaling up Test-Time Compute with Latent Reasoning: A Recurrent Depth Approach

## TL;DR

A novel LM architecture that scales test-time compute by *iterating a recurrent transformer block* — unrolling to arbitrary depth at inference. Trained on standard pretraining data (no specialized CoT supervision), works with small context windows, and the resulting 3.5B-parameter "Huginn" model effectively uses up to 50B-parameter-equivalent compute for hard reasoning. NeurIPS 2025 spotlight.

## Claims

- Test-time compute can scale *vertically* (more passes through a recurrent block in latent) instead of *horizontally* (more tokens) — the two are not equivalent.
- The vertical-scaling regime captures reasoning that doesn't fit cleanly in words. No specialized training data needed; the model learns to use deeper unrolling for harder problems on its own.
- A single architecture handles both quick and deliberate reasoning by varying the unroll depth — a continuous knob, not a regime switch.

## Methods

- Recurrent transformer block: a stack of transformer layers reused multiple times during the forward pass with the residual stream as the recurrent state.
- 3.5B parameters, 800B tokens trained, standard LM objective.
- Test-time: unroll the recurrent block more or fewer times depending on the problem.

## Results

- Significant gains on math and code with deeper unrolling; up to 50B-parameter-equivalent performance from a 3.5B model.
- No specialized training data — the same model handles fast tasks at low depth and hard tasks at high depth.
- Behavior is reasonable on small context windows, unlike many CoT regimes.

## Critique / open questions

- Recurrent-block training is harder to optimize than standard transformer training (vanishing/exploding gradients).
- Deeper unrolling helps on hard reasoning; less clear it composes naturally with retrieval or tool use.
- "How deep is enough" is implicit — no learned termination signal; the user picks depth at inference.

## Follow-up

**Relevance:** 5 — the cleanest existence proof that *all cognition can live in latent* with no token-mediated reasoning supervision. Strongest single counterargument to the "token bottleneck as inductive bias" worry in NOTES.md (open question #5): the model trained without token-CoT scaling beats CoT at scale, suggesting the bottleneck isn't load-bearing for OOD generalization.

- Model: huggingface.co/tomg-group-umd/huginn-0125. Code: github.com/seal-rg/recurrent-pretraining.
- Recurrent depth + retrieval-as-layer is a natural composition this project should explore — recurrent depth gives compute, retrieval-as-layer gives knowledge. Neither has been combined yet.
