---
kind: paper
title: "Large Language Diffusion Models (LLaDA)"
authors: ["Shen Nie", "Fengqi Zhu", "Zebin You", "Xiaolu Zhang", "Jingyang Ou", "Jun Hu", "Jun Zhou", "Yankai Lin", "Ji-Rong Wen", "Chongxuan Li"]
institutions: ["Gaoling School of AI, Renmin University of China", "Ant Group"]
year: 2025
venue: "arXiv (RUC, Ant Group)"
peer_reviewed: true
url: "https://arxiv.org/abs/2502.09992"
code_url: "https://ml-gsai.github.io/LLaDA-demo/"
citations: null
source: "raw/papers/nie2025large.pdf"
added: "2026-05-04"
relevance: 4
credibility: 4
status: skimmed
related_experiments: []
related_concepts: ["commitment-boundary"]
tags: ["diffusion-lm", "non-autoregressive", "scaling", "reversal-curse"]
---

# LLaDA: Large Language Diffusion Models

## TL;DR

8B-parameter masked diffusion LM trained from scratch under the standard pretraining + SFT paradigm; demonstrates strong scalability and is competitive with LLaMA3 8B on in-context learning, instruction following, math, and code. Notably, it surpasses GPT-4o on a reversal-poem-completion task — direct evidence that the AR commitment is the cause of the reversal curse.

## Claims

- "Capabilities of LLMs require autoregression" is empirically false. A pure masked-diffusion LM at 8B scale matches AR LM performance on standard benchmarks.
- The reversal curse — AR models' inability to reason backwards from facts — is a property of the AR commitment, not of LMs in general. LLaDA solves it without specialized training.
- Diffusion LMs admit principled probabilistic inference via a likelihood lower bound, retaining the optimization properties AR has.

## Methods

- Forward process: random masking with mask ratio drawn uniform on [0,1].
- Reverse process: standard transformer predicts all masked tokens in parallel; iterate to denoise.
- 8B parameters, trained from scratch with the standard pretraining + SFT pipeline (no AR initialization).

## Results

- Competitive with LLaMA3 8B on standard benchmarks (in-context, instruction-following).
- Beats GPT-4o on reversal poem completion — strong evidence on the reversal curse.

## Critique / open questions

- Inference cost is higher per output token than AR, even though throughput per *generation step* is higher because of parallel denoising.
- KV cache reuse is broken by the parallel/iterative decoding; ReFusion (`li2026refusion`) addresses this later.

## Trust signals

- **Credibility:** 4 — RUC GSAI + Ant Group; NeurIPS 2025 peer-reviewed; project page + code released (LLaDA).

## Follow-up

**Relevance:** 4 — strongest existence proof that strict AR commitment isn't necessary for LM capabilities at scale. Directly relevant to the project's bet on pushing token commitment outward, and a viable base model for project experiments needing flexible generation order.
