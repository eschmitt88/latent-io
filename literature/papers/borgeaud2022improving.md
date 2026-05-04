---
kind: paper
title: "Improving language models by retrieving from trillions of tokens (RETRO)"
authors: ["Sebastian Borgeaud", "Arthur Mensch", "Jordan Hoffmann", "et al."]
year: 2022
venue: "ICML 2022 (DeepMind)"
url: "https://arxiv.org/abs/2112.04426"
source: "raw/papers/borgeaud2022improving.pdf"
added: "2026-05-04"
relevance: 4
status: skimmed
related_experiments: []
related_concepts: ["retrieval-as-layer", "latent-index"]
tags: ["foundational", "rag", "chunked-cross-attention", "retrieval-pretraining"]
---

# RETRO: Retrieval-Enhanced Transformer

## TL;DR

DeepMind's foundational retrieval-augmented decoder: tokens are partitioned into chunks, each chunk retrieves k neighbours of r tokens from a frozen-BERT-encoded 2T-token corpus, and a chunked cross-attention module integrates the neighbours with linear time complexity in retrieved data. Achieves GPT-3-comparable performance on the Pile with 25× fewer parameters.

## Claims

- Retrieval can be made a *training-time* augmentation rather than a turn-time one — the model is pretrained from scratch with retrieved neighbours always available.
- Chunked cross-attention is structurally efficient: attention cost is linear in retrieved data because neighbour and time dimensions are merged before attending.
- A frozen retriever (BERT) plus a differentiable encoder is a sufficient training signal — the retriever doesn't need to be updated jointly.
- Retrieval scales with database size: 2T-token retrieval gives a 25× parameter-efficiency boost.

## Methods

- Sequence of length n split into l chunks. For each chunk, retrieve k neighbours of r tokens each from a BERT-encoded corpus.
- Chunked cross-attention block integrates neighbours into the decoder; runs at fine-grained passage level while regular self-attention handles document-level coherence.
- Can also "RETROfit" pretrained transformers — bolt retrieval onto a frozen base with light fine-tuning.

## Results

- 2T-token retrieval, 25× param efficiency vs. GPT-3 on Pile perplexity.
- Strong on knowledge-intensive QA after fine-tuning.

## Critique / open questions

- Retriever is frozen BERT — gradients don't flow back, so the retriever can't co-adapt with the generator (the problem CLaRa later solves).
- Cross-attention happens at the *token* level on retrieved text — still token-mediated, not latent-vector retrieval. RETRO is the closest token-side ancestor of design-move 3, not its instantiation.
- Test-time retrieval over a 2T-token store has nontrivial infrastructure cost; the paper assumes it as given.

## Follow-up

**Relevance:** 4 — foundational. Required reading to understand what "retrieval as a layer" looked like *before* the field went latent. Comparing RETRO's chunked cross-attention against CLaRa's memory-token / LAnR's `[PRED]`-vector approaches is the natural way to reason about where the project sits in the design space.
