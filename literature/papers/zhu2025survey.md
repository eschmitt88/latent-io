---
kind: paper
title: "A Survey on Latent Reasoning"
authors: ["Rui-Jie Zhu", "Tianhao Peng", "Tianhao Cheng", "Xingwei Qu", "Jiaheng Liu", "Ge Zhang", "Wenhao Huang", "Jason Eshraghian", "et al."]
institutions: ["M-A-P", "UCSC", "Fudan / NJU / PKU / RUC / U. Manchester / UW-Madison / PolyU (multi-institution)"]
year: 2025
venue: "arXiv (M-A-P, UCSC, multi-institution)"
peer_reviewed: false
url: "https://arxiv.org/abs/2507.06203"
code_url: "https://github.com/multimodal-art-projection/LatentCoT-Horizon"
citations: null
source: "raw/papers/zhu2025survey.pdf"
added: "2026-05-04"
relevance: 3
credibility: 3
status: skimmed
related_experiments: []
related_concepts: ["continuous-thought"]
tags: ["survey", "latent-reasoning", "M-A-P", "field-orientation"]
---

# A Survey on Latent Reasoning (M-A-P)

## TL;DR

Comprehensive survey arguing that token-level CoT bottlenecks expressive bandwidth and that latent reasoning eliminates that bottleneck by performing multi-step inference in continuous hidden states. Covers continuous-thought (Coconut and successors), recurrent-depth approaches, implicit reasoning via distillation, latent compression, and theoretical foundations.

## Claims (as a survey)

- Latent reasoning is an emerging field, not just a collection of one-off techniques. A unified taxonomy is possible: continuous-thought, recurrent-depth, implicit-distilled, hybrid text-latent.
- Token-level CoT trades expressive bandwidth (one symbol per step) for interpretability and gradient-friendliness; latent reasoning recovers the bandwidth at the cost of opacity.

## Methods (as a survey)

- Field-oriented taxonomy + exhaustive citation list.
- Companion repo: `multimodal-art-projection/LatentCoT-Horizon` — curated paper list.

## Results

N/A — survey.

## Critique / open questions

- Field is moving fast; surveys decay quickly. Use as orientation, not as the primary read.

## Trust signals

- **Credibility:** 3 — M-A-P + UCSC multi-institution; arXiv preprint, no peer review; companion paper-collection repo (LatentCoT-Horizon).

## Follow-up

**Relevance:** 3 — orientation. Read once when seeding `concepts/`; the companion repo is the standing index for new entries.
