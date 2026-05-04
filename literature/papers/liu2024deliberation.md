---
kind: paper
title: "Deliberation in Latent Space via Differentiable Cache Augmentation"
authors: ["Luyang Liu", "Jonas Pfeiffer", "Jiaxing Wu", "Jun Xie", "Arthur Szlam"]
year: 2024
venue: "arXiv (Google DeepMind)"
url: "https://arxiv.org/abs/2412.17747"
source: "raw/papers/liu2024deliberation.pdf"
added: "2026-05-04"
relevance: 5
status: skimmed
related_experiments: []
related_concepts: ["action-observation-trace", "continuous-thought", "retrieval-as-layer"]
tags: ["frozen-decoder", "kv-cache", "coprocessor", "asynchronous", "deepmind"]
---

# Deliberation in Latent Space via Differentiable Cache Augmentation

## TL;DR

A frozen LLM is augmented with an offline coprocessor that operates on the model's KV cache, injecting a set of latent embeddings learned end-to-end via the standard LM loss while keeping the decoder frozen. The coprocessor runs asynchronously, the decoder works without it, and cache augmentation reduces perplexity and improves performance on reasoning tasks with no task-specific training.

## Claims

- Standard reasoning techniques (CoT, scratchpads) generate discrete tokens immediately before responding, incurring latency and being hard to optimize end-to-end.
- A frozen LLM's KV cache is the natural injection site for additional latent computation: it preserves the existing model's behavior, supports asynchronous offline computation, and is differentiable end-to-end through the standard LM loss.
- The coprocessor learns *how* to deposit useful computation into the cache without the decoder being modified — i.e. the cache is the *interface*; the decoder is unchanged.
- Cache augmentation works without task-specific training — generic improvement on reasoning tasks.

## Methods

- Train a small coprocessor that takes a KV cache as input and produces a set of latent embeddings to append.
- Loss: standard next-token LM loss from the (frozen) decoder operating on the augmented cache; gradients flow only into the coprocessor.
- Inference: coprocessor runs offline / asynchronously; decoder uses augmented cache when available, plain cache otherwise.

## Results

- Lower perplexity on subsequent tokens when cache is augmented.
- Cross-task gains on reasoning benchmarks without task-specific training.
- Decoder remains usable without the coprocessor — graceful fallback.

## Critique / open questions

- The "tool" here is a generic computational augmentation, not a typed external operation (retrieval, code execution). Generalizing to tool-use means designing per-tool coprocessors or learning routing.
- Asynchrony is presented as a feature; for action–observation traces (NOTES.md design-move 4), the timing of the augmentation matters and cannot be fully decoupled.

## Follow-up

**Relevance:** 5 — closest existing work to "tool use as a continuous primitive" in the project's exact sense. The KV-cache augmentation pattern is the cleanest mechanism for injecting latent results into a frozen base model — directly applicable to retrieval, tool returns, or learned auxiliary computation. Anchors the new `action-observation-trace` concept and ties into `continuous-thought` and `retrieval-as-layer`.

- The asynchronous-coprocessor pattern is an elegant solution to NOTES.md's long-horizon coherence question: a separate latent process can update the cache as new evidence arrives, without forcing the main decoder to re-plan.
- Read carefully when designing the project's first action-observation-trace experiment.
