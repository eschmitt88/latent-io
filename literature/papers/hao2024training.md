---
kind: paper
title: "Training Large Language Models to Reason in a Continuous Latent Space (Coconut)"
authors: ["Shibo Hao", "Sainbayar Sukhbaatar", "DiJia Su", "Xian Li", "Zhiting Hu", "Jason Weston", "Yuandong Tian"]
year: 2024
venue: "NeurIPS 2024 (FAIR Meta, UCSD)"
url: "https://arxiv.org/abs/2412.06769"
source: "raw/papers/hao2024training.pdf"
added: "2026-05-04"
relevance: 5
status: skimmed
related_experiments: []
related_concepts: ["continuous-thought", "commitment-boundary"]
tags: ["latent-reasoning", "coconut", "bfs", "foundational"]
---

# Coconut: Chain of Continuous Thought

## TL;DR

Replace token-level chain-of-thought with continuous-thought: feed the model's last hidden state directly back as the next input embedding instead of decoding it to a word. The continuous thought encodes a *superposition* of alternative next steps, enabling latent breadth-first search and outperforming text-CoT on logical reasoning tasks that need substantial planning, while generating fewer tokens.

## Claims

- Language space is not always optimal for reasoning. Most word tokens carry textual coherence weight that is irrelevant to the underlying computation; a few critical tokens carry hard planning that single-token sampling collapses prematurely.
- A continuous thought (last-layer hidden state, fed back as next input embedding) encodes alternative next steps in superposition — the model can explore branches before committing.
- Coconut outperforms CoT on logical reasoning tasks that need substantial search; the gap is widest where token-CoT's premature commitment hurts most.
- Latent reasoning trades fewer tokens for more compute per token — a different point on the efficiency curve, not strictly cheaper.

## Methods

- During training, the model alternates between generating "continuous thoughts" (no decoding) and standard token outputs.
- Inference: emit continuous thoughts for some number of steps before producing the textual answer; thoughts are last-layer hidden states recycled as the next input embedding.
- Evaluated on math (GSM8k), logical reasoning (ProsQA), and planning tasks.

## Results

- Strong gains over CoT on logical reasoning where planning matters; comparable or better on tasks that don't.
- Generation is shorter (fewer tokens) at competitive accuracy.
- Probing analysis shows continuous thoughts encode multiple alternative next steps simultaneously.

## Critique / open questions

- Continuous thoughts are uninterpretable in the strict sense (NOTES.md open question #2). The paper's probes are useful but not a full debugging story.
- Training requires the alternating regime — bolting continuous thoughts onto a frozen model is harder.
- The "superposition" interpretation is empirical; the formal theoretical grounding came later (`zhu2025reasoning`).

## Follow-up

**Relevance:** 5 — the load-bearing demonstration that latent reasoning is computationally different from token reasoning, not just an efficiency variant. Anchors the `continuous-thought` and `commitment-boundary` concepts. Code at github.com/facebookresearch/coconut.

- The probing methodology (decoding the latent thought to recover candidate next-step tokens) is directly transferable as a debugging tool for the project's latent operations.
- Pair against `zhu2025reasoning` for the theoretical justification.
