---
kind: paper
title: "Mercury: Ultra-Fast Language Models Based on Diffusion"
authors: ["Samar Khanna", "Siddhant Kharbanda", "Shufan Li", "Harshit Varma", "Eric Wang", "Sawyer Birnbaum", "Ziyang Luo", "Yanis Miraoui", "Akash Palrecha", "Stefano Ermon", "Aditya Grover", "Volodymyr Kuleshov"]
institutions: ["Inception Labs"]
year: 2025
venue: "arXiv (Inception Labs)"
peer_reviewed: false
url: "https://arxiv.org/abs/2506.17298"
code_url: null
citations: null
source: "raw/papers/khanna2025mercury.pdf"
added: "2026-05-04"
relevance: 3
credibility: 3
status: skimmed
related_experiments: []
related_concepts: []
tags: ["commercial", "diffusion-lm", "code-generation", "speed", "deployment"]
---

# Mercury: Ultra-Fast Diffusion LLMs

## TL;DR

Inception Labs' commercial-scale diffusion LLM family. Mercury Coder Mini and Small reach 1109 / 737 tok/s on H100s — outperforming speed-optimized frontier models by up to 10× while matching their quality on coding benchmarks. Currently #2 on Copilot Arena quality and #1 on speed.

## Claims

- A diffusion LLM can be deployed at commercial scale with quality competitive with speed-optimized frontier AR models.
- Parallel multi-token prediction is the key throughput unlock; Mercury is parameterized via the Transformer architecture but trained for parallel decoding.
- Real-world validation: Copilot Arena ranks Mercury #2 on quality, #1 on speed.

## Methods

- Transformer-based diffusion LLM trained for parallel multi-token prediction.
- Two sizes (Mini, Small) with corresponding speed/quality tradeoffs.

## Results

- 1109 / 737 tok/s on H100 (Mini / Small).
- Up to 10× faster than speed-optimized AR baselines at comparable quality.
- Public API + free playground.

## Critique / open questions

- Technical report; full training details and architecture choices are not exhaustively documented.
- Model weights are commercial — not directly usable as a project base model.

## Trust signals

- **Credibility:** 3 — Inception Labs commercial tech report; arXiv preprint, no peer review; closed model, no code (API only). Independent third-party benchmarks add some weight.

## Follow-up

**Relevance:** 3 — evidence that the non-AR commitment regime is production-viable, useful as motivation in proposals. Not directly usable as an experiment base.
