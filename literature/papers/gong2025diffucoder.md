---
kind: paper
title: "DiffuCoder: Understanding and Improving Masked Diffusion Models for Code Generation"
authors: ["Shansan Gong", "Ruixiang Zhang", "Huangjie Zheng", "Jiatao Gu", "Navdeep Jaitly", "Lingpeng Kong", "Yizhe Zhang"]
year: 2025
venue: "arXiv (Apple, HKU)"
url: "https://arxiv.org/abs/2506.20639"
source: "raw/papers/gong2025diffucoder.pdf"
added: "2026-05-04"
relevance: 4
status: skimmed
related_experiments: []
related_concepts: ["commitment-boundary"]
tags: ["diffusion-lm", "code-generation", "AR-ness", "coupled-grpo", "non-left-to-right"]
---

# DiffuCoder: Masked Diffusion for Code

## TL;DR

7B masked diffusion LM trained on 130B tokens of code; the paper systematically analyzes how dLLM decoding differs from AR on code, defining an "AR-ness" metric showing that dLLMs become *less* left-to-right when generating code. Introduces coupled-GRPO, an RL algorithm respecting the non-AR objective via coupled sampling.

## Claims

- Code is structurally non-sequential; AR's strict left-to-right commitment is suboptimal for it.
- dLLMs naturally exhibit *less* AR-ness on code than on natural language — they learn that generation order can be reordered when it helps.
- Increasing sampling temperature diversifies *both* token choice and generation order, creating a richer search space for RL rollouts.
- Coupled-GRPO (a coupled-sampling RL technique) respects the non-AR objective and outperforms vanilla GRPO for diffusion LMs.

## Methods

- 7B parameter masked diffusion LM, 130B token code-pretraining corpus.
- AR-ness metric: measures how closely the model's actual generation order tracks left-to-right.
- Coupled-GRPO: pairs sampled trajectories to reduce log-likelihood variance for non-AR RL.

## Results

- Strong code performance, with substantially non-left-to-right generation order on complex algorithmic tasks.
- Coupled-GRPO improves on standard RL for diffusion LMs.

## Critique / open questions

- AR-ness metric is descriptive; whether non-AR generation *causes* the quality gain or just correlates with it is not isolated.
- 7B is small enough to be trainable in academia but the comparison against frontier code LMs is constrained.

## Follow-up

**Relevance:** 4 — directly relevant to the cross-file completion experiment proposed in NOTES.md. The AR-ness metric is exactly the kind of measurement the project will need to argue tokens are bottlenecking latent cognition. Code at github.com/apple/ml-diffucoder.
