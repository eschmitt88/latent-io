---
kind: paper
title: "SpiralThinker: Latent Reasoning through an Iterative Process with Text–Latent Interleaving"
authors: ["Shengmin Piao", "Sanghyun Park"]
institutions: ["Yonsei University"]
year: 2025
venue: "arXiv (Yonsei University)"
peer_reviewed: false
url: "https://arxiv.org/abs/2511.08983"
code_url: "https://github.com/shengminp/SpiralThinker"
citations: null
source: "raw/papers/piao2025spiralthinker.pdf"
added: "2026-05-04"
relevance: 4
credibility: 3
status: skimmed
related_experiments: []
related_concepts: ["continuous-thought", "commitment-boundary"]
tags: ["latent-reasoning", "iterative", "text-latent-interleaving", "alignment"]
---

# SpiralThinker: Iterative Latent Reasoning with Text–Latent Interleaving

## TL;DR

A stabilized iterative-latent-reasoning framework that performs progressive updates over latent representations interleaved with explicit textual reasoning steps. A *progressive alignment objective* explicitly regulates latent representations across iterations, and structured annotations supervise the interleaving — addressing two pain points of latent-only reasoning: instability of latent updates and lack of a principled way to mix implicit and explicit steps. SOTA on GSM8K-Aug (56.56%), ProsQA (99.40%), StrategyQA (63.32%) among latent methods.

## Claims

- Existing latent-only reasoning is unstable across iterations — latent representations drift without an explicit regularizer.
- Latent reasoning should be *iterative*, not a one-shot continuous-thought emission. Multiple passes refine the representation.
- Text and latent reasoning should *interleave* — text steps act as anchoring commitments that prevent latent drift while latent steps provide computation density between them.

## Methods

- Prepend N `<latent>` tokens at the start of the question to initiate implicit reasoning; the model processes them iteratively before generating text.
- After each text step, the model autonomously inserts more `<latent>` tokens, alternating until termination.
- Progressive alignment objective: latent representations across iterations are regularized to follow a coherent trajectory rather than drifting.
- Structured annotations supervise where the latent/text interleaves should occur.

## Results

- GSM8K-Aug 56.56%, ProsQA 99.40%, StrategyQA 63.32% — SOTA among latent reasoning methods.
- Stability ablations show the alignment objective is necessary; without it, latent representations drift incoherently.

## Critique / open questions

- The "structured annotations" requirement is significant overhead — supervises *where* to interleave, which the project's vision wants the model to figure out.
- The alignment regularizer constrains latent representations to be coherent across iterations; whether this loses some of Coconut's superposition benefit is unstudied.
- Inference: starts with a fixed number `N` of latent tokens; not adaptive.

## Trust signals

- **Credibility:** 3 — Yonsei University; arXiv preprint, no peer review; official code released (shengminp/SpiralThinker).

## Follow-up

**Relevance:** 4 — most directly relevant to the membrane framing's claim that text appears only at *commitment boundaries* while cognition happens in latent. The interleaving training scheme is a candidate template for design-move 4 (action–observation traces) — text plays the role of "commitment" between latent computation phases.
