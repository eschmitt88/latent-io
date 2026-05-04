---
kind: paper
title: "Latent Abstraction for Retrieval-Augmented Generation (LAnR)"
authors: ["Ha Lan N.T", "Minh-Anh Nguyen", "Dung D. Le"]
year: 2026
venue: "arXiv (VinUniversity)"
url: "https://arxiv.org/abs/2604.17866"
source: "raw/papers/lan2026latent.pdf"
added: "2026-05-04"
relevance: 5
status: skimmed
related_experiments: []
related_concepts: ["latent-query", "latent-index", "uncertainty-trigger", "retrieval-as-layer"]
tags: ["latent-retrieval", "rag", "uncertainty", "multi-hop", "membrane"]
---

# Latent Abstraction for Retrieval-Augmented Generation (LAnR)

## TL;DR

A single LLM performs encoding, retrieval, and generation entirely in its own latent space: a designated `[PRED]` token's hidden state becomes a dense retrieval vector matched against documents encoded by the same model, and a lightweight MLP head over the same hidden states decides when retrieval is sufficient — driven by the empirical observation that answer-token entropy reliably signals retrieval sufficiency. Outperforms text-query RAG on six QA benchmarks with fewer retrieval calls.

## Claims

- Generating natural-language queries between hops collapses the model's full uncertainty distribution into a single sampled trajectory, throwing away the alternative reasoning paths that latent representations can hold in superposition.
- A single model can simultaneously serve as encoder, retriever, and generator without architectural separation — same weights, different read-out heads on the residual stream.
- Answer-token entropy is a reliable, training-free signal for retrieval sufficiency. An MLP control head over hidden states learns to predict it directly, replacing explicit "should I retrieve more?" token-level reasoning.
- Implicit retrieval reduces the *number* of retrieval calls relative to explicit-CoT baselines while improving accuracy — the latent-side commitment is cheaper.

## Methods

- Single LLM is repurposed three ways via different read-outs: (i) encode documents into vector representations; (ii) at a `[PRED]` token, read out a query vector; (iii) decode the answer.
- Retrieval is dot-product matching between the `[PRED]` hidden state and document representations from the same model.
- Sufficiency control: a small MLP over the `[PRED]` hidden state classifies "retrieve again" vs. "answer now". Trained against a target derived from answer-token entropy on a held-out set.
- Eval on six QA benchmarks across single-hop and multi-hop settings.

## Results

- Outperforms RAG baselines while requiring fewer retrieval calls on multi-hop benchmarks.
- The MLP control head's behavior tracks answer-entropy curves cleanly — the empirical motivation holds in practice.

## Critique / open questions

- Single-model encode+retrieve+generate ties the index encoder to the generator's training; live-encoding new documents during deployment requires the generator's encoding head to remain stable as the model is updated. The embedding-compatibility open question (NOTES.md #1) is not solved here, only side-stepped.
- Sufficiency-from-entropy is elegant but can be fooled by confidently-wrong answers — the head learns to predict entropy, not correctness.
- Scaling: tested on QA benchmarks; behavior under long-form generation, code, or settings where "sufficient evidence" is ill-defined isn't characterized.

## Follow-up

**Relevance:** 5 — fuses design-moves 1 and 2 cleanly. The `[PRED]`-token query and the entropy-driven MLP head are concrete templates for `latent-query` and a new `uncertainty-trigger` concept respectively.

- The entropy-as-sufficiency signal is the most interesting transferable finding here; worth replicating before assuming it generalizes.
- Pair this against CLaRa (`he2025bridging`) — both have latent queries; CLaRa keeps generator and retriever as separate LoRA adapters on a shared base, LAnR makes them *literally* the same weights with different read-outs. The right design point for a project experiment is somewhere in this spectrum.
