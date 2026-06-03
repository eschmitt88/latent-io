---
kind: paper
title: "Dream-Coder 7B: An Open Diffusion Language Model for Code"
authors: ["Zhihui Xie", "Jiacheng Ye", "Lin Zheng", "Jiahui Gao", "Jingwei Dong", "Zirui Wu", "Xueliang Zhao", "Shansan Gong", "Xin Jiang", "Zhenguo Li", "Lingpeng Kong"]
institutions: ["The University of Hong Kong", "Huawei Noah's Ark Lab"]
year: 2025
venue: "arXiv (HKU, Huawei Noah's Ark)"
peer_reviewed: false
url: "https://arxiv.org/abs/2509.01142"
code_url: "https://github.com/DreamLM/Dream-Coder"
citations: null
source: "raw/papers/xie2025dream.pdf"
added: "2026-05-04"
relevance: 4
credibility: 4
status: skimmed
related_experiments: []
related_concepts: ["commitment-boundary"]
tags: ["diffusion-lm", "code-generation", "any-order", "open-model", "rl-with-verifiable-rewards"]
---

# Dream-Coder 7B: Open Diffusion LM for Code

## TL;DR

Open-source 7B discrete diffusion LM for code, with emergent any-order generation: adapts decoding strategy by task — sketch-first for complex algorithms, left-to-right for straightforward completions, interleaved reasoning for code understanding. Adapts a pretrained AR checkpoint to discrete diffusion via continuous-time weighted CE; post-trained with SFT (random truncation + padding penalty) and RL with verifiable rewards.

## Claims

- A single diffusion LM can learn task-conditional decoding strategies — generation order isn't a fixed property of the model but an emergent capability.
- AR-pretrained checkpoints can be adapted to diffusion via continuous-time weighted cross-entropy; you don't need to train from scratch.
- Padding pathologies are a major SFT failure mode for diffusion LMs; random truncation + a padding penalty stabilize generation.

## Methods

- Init: AR pretrained checkpoint → diffusion via continuous-time weighted CE adaptation.
- SFT: random truncation, padding penalty.
- RL: verifiable rewards (compile, test pass) over curated open-source prompts.

## Results

- 21.4% pass@1 on LiveCodeBench (2410–2505).
- Competitive on HumanEval, MBPP.
- Demonstrates task-adaptive decoding (sketch / LTR / interleaved).

## Critique / open questions

- "Any-order" is qualitative; the paper doesn't fully characterize when each strategy emerges.
- AR-to-diffusion adaptation is appealing but loses some properties of from-scratch training (e.g. LLaDA's reversal-curse fix).

## Trust signals

- **Credibility:** 4 — HKU + Huawei Noah's Ark; arXiv preprint, not yet peer-reviewed; open model + code/checkpoints released (DreamLM/Dream-Coder).

## Follow-up

**Relevance:** 4 — open alternative to DiffuCoder for the planned cross-file code-completion experiment. The task-conditional decoding strategy is concretely the kind of "commitment policy" the project needs to study at the membrane.
