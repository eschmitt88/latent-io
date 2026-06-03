---
kind: paper
title: "Autoregressive vs. Masked Diffusion Language Models: A Controlled Comparison"
authors: ["Caio Vicentino"]
institutions: ["Independent Researcher"]
year: 2026
venue: "arXiv (independent)"
peer_reviewed: false
url: "https://arxiv.org/abs/2603.22075"
code_url: "https://github.com/caiovicentino/arche"
citations: null
source: "raw/papers/vicentino2026autoregressive.pdf"
added: "2026-05-04"
relevance: 2
credibility: 2
status: skimmed
related_experiments: []
related_concepts: []
tags: ["controlled-experiment", "ar-vs-mdm", "tinystories", "diversity-fluency-tradeoff"]
---

# Autoregressive vs. Masked Diffusion: A Controlled Comparison

## TL;DR

Independent controlled comparison of AR vs. MDLM at matched data (50M TinyStories tokens), compute (20K steps × batch 32 × seq 512), and hardware (single H100). Three findings: (1) MDLM has only 4.7% wall-clock overhead vs. AR; (2) AR converges faster but overfits earlier, MDLM converges slowly and is still improving at step 20K; (3) AR is fluent-but-repetitive (99.8% same opening word), MDLM is more diverse (93.4% unique 5-word openings) at the cost of occasional grammar errors.

## Claims

- "Diffusion is much more expensive than AR" is empirically false at matched compute — it's only ~5% more expensive in wall-clock at small scale.
- AR and MDLM have *different* compute-optimal regimes: AR overfits early, MDLM benefits from longer training.
- There's a structural diversity–fluency tradeoff between the paradigms — neither is strictly better; they make different tradeoffs.

## Methods

- TinyStories 50M tokens; identical compute budget; identical hardware; isolation of generation paradigm as the sole variable.
- 1000 generated samples per model for diversity analysis (Distinct-n, Self-BLEU).

## Results

- Throughput: AR ~50K tok/s, MDLM ~50K tok/s with 4.7% extra wall time.
- Diversity: MDLM 93.4% unique 5-word openings vs. AR 99.8% same opening word.

## Critique / open questions

- TinyStories scale is small; whether the diversity–fluency split holds at frontier scale isn't tested.
- Validation losses across paradigms aren't directly comparable (different objectives) — the paper acknowledges this.

## Trust signals

- **Credibility:** 2 — Independent single author; arXiv preprint, no peer review; code released (caiovicentino/arche). Full code release lifts an otherwise weak prior.

## Follow-up

**Relevance:** 2 — methodologically useful template for any project experiment that argues "latent/non-AR helps". A small, clean controlled comparison is the right way to make such a claim. The diversity-fluency tradeoff finding is interesting and worth replicating.
