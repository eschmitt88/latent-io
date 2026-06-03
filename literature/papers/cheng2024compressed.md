---
kind: paper
title: "Compressed Chain of Thought: Efficient Reasoning through Dense Representations"
authors: ["Jeffrey Cheng", "Benjamin Van Durme"]
institutions: ["Johns Hopkins University"]
year: 2024
venue: "arXiv (JHU)"
peer_reviewed: false
url: "https://arxiv.org/abs/2412.13171"
code_url: null
citations: null
source: "raw/papers/cheng2024compressed.pdf"
added: "2026-05-04"
relevance: 3
credibility: 3
status: skimmed
related_experiments: []
related_concepts: ["continuous-thought", "commitment-boundary"]
tags: ["compressed-cot", "contemplation-tokens", "variable-length"]
---

# Compressed Chain of Thought (CCoT)

## TL;DR

Generates "contentful, continuous, variable-length contemplation tokens" — compressed representations of explicit reasoning chains — as a drop-in for textual CoT, applicable to off-the-shelf decoder LMs. Reasoning improvements scale with the number of contemplation tokens, giving an on-demand accuracy/efficiency knob.

## Claims

- Contemplation tokens (a term the paper coins) are special tokens emitted at inference for extra compute; prior work used fixed-length sequences from a discrete embedding set, which limits expressivity.
- Variable-length, continuous contemplation tokens are strictly more expressive — they can carry more reasoning per slot.
- The technique is bolt-on: works with off-the-shelf decoder LMs without retraining the base.

## Methods

- A small head produces variable-length sequences of dense contemplation embeddings, conditioned on the input.
- The contemplation tokens are inserted into the model's residual stream (mid-prefix, before decoding the answer).

## Results

- Accuracy improves with number of contemplation tokens generated.
- Adaptive — on easy inputs the model can produce few tokens, more on hard inputs.

## Critique / open questions

- Variable-length policy is learned implicitly; no explicit uncertainty-driven termination criterion.
- "Contemplation tokens" overlap conceptually with Coconut's continuous thoughts and pause tokens — unclear what unique mechanism CCoT contributes beyond variable length.

## Trust signals

- **Credibility:** 3 — JHU NLP group; arXiv preprint, no peer review; no code link in note. Reputable group, partial signals.

## Follow-up

**Relevance:** 3 — useful comparison point for the project's design space at the latent–token boundary. The variable-length angle is the most distinctive contribution.
