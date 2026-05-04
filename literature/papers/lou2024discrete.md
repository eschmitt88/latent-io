---
kind: paper
title: "Discrete Diffusion Modeling by Estimating the Ratios of the Data Distribution (SEDD)"
authors: ["Aaron Lou", "Chenlin Meng", "Stefano Ermon"]
year: 2024
venue: "ICML 2024 Best Paper (Stanford)"
url: "https://arxiv.org/abs/2310.16834"
source: "raw/papers/lou2024discrete.pdf"
added: "2026-05-04"
relevance: 3
status: skimmed
related_experiments: []
related_concepts: []
tags: ["foundational", "score-entropy", "discrete-diffusion", "icml-best-paper"]
---

# SEDD: Score Entropy Discrete Diffusion

## TL;DR

Introduces *score entropy*, a novel loss that extends score matching to discrete spaces and seamlessly fits into discrete diffusion models — a 25–75% perplexity reduction over prior diffusion LMs and competitive with autoregressive models. Around 6–8× better generative perplexity than un-annealed GPT-2, with 32× fewer network evaluations at matched quality and controllable infilling.

## Claims

- Standard score matching doesn't generalize cleanly to discrete data; prior efforts gave smaller gains than expected.
- A new loss — score entropy — is the natural discrete analogue and integrates seamlessly with discrete diffusion architectures.
- Discrete diffusion can match or beat AR on language modeling perplexity and supports controllable generation (infilling, non-left-to-right) that AR cannot.

## Methods

- Score entropy: a loss that estimates the ratios of the data distribution at neighboring discrete states.
- Standard transformer parameterization with the score-entropy objective.

## Results

- 25–75% perplexity reduction vs. prior discrete diffusion LMs.
- 6–8× better generative perplexity than un-annealed GPT-2.
- 32× fewer network evaluations at matched quality (compute–quality tradeoff knob).
- Controllable infilling matches nucleus-sampling quality in left-to-right while enabling other generation orders.

## Critique / open questions

- Theoretical contribution; large-scale instantiation came from later work (LLaDA, MDLM).
- "Controllable" generation is a property of the framework but the practical scope of the control isn't characterized.

## Follow-up

**Relevance:** 3 — theoretical foundation. Required reading to understand what the loss function is actually doing in modern diffusion LMs; useful when designing the project's own latent training objective if it ends up using a diffusion-style noise schedule.
