---
kind: paper
title: "Think before you speak: Training Language Models With Pause Tokens"
authors: ["Sachin Goyal", "Ziwei Ji", "Ankit Singh Rawat", "Aditya Krishna Menon", "Sanjiv Kumar", "Vaishnavh Nagarajan"]
institutions: ["Carnegie Mellon University", "Google Research"]
year: 2024
venue: "ICLR 2024 (CMU, Google Research)"
peer_reviewed: true
url: "https://arxiv.org/abs/2310.02226"
code_url: null
citations: null
source: "raw/papers/goyal2024think.pdf"
added: "2026-05-04"
relevance: 4
credibility: 4
status: skimmed
related_experiments: []
related_concepts: ["continuous-thought"]
tags: ["foundational", "pause-token", "extra-compute", "iclr-2024"]
---

# Think Before You Speak: Pause Tokens

## TL;DR

Append a learnable "pause" token to the input prefix and delay output extraction until the last pause token is seen — granting the model extra hidden-state computation without requiring more output tokens. Empirically, pause-training (both pretraining and fine-tuning) gives non-trivial gains on reasoning, QA, and general understanding tasks at 1B and 130M scale.

## Claims

- The (K+1)th token in a transformer is the result of K hidden-vector manipulations; if we let the model manipulate K+10 hidden vectors first, it can reason more before committing.
- The mechanism doesn't require learning anything except how to use the extra compute — just appending pauses and delaying output extraction is enough, given training-time exposure.
- Gains require *both* pretraining and fine-tuning with pauses; fine-tune-only gives less.

## Methods

- Add a learnable embedding for `<pause>`; append a sequence of them to inputs at training time. At inference, extract output only after the final pause.
- Train decoder-only models (130M, 1B) on C4 with causal LM, with and without pauses.
- Eval on reasoning, QA, general understanding, fact recall.

## Results

- Consistent gains across tasks, with pretraining-with-pauses being necessary for the largest effects.
- Fine-tune-only gains exist but are smaller.

## Critique / open questions

- Mechanism is opaque — *what* the model does with the extra compute isn't characterized; the empirical bump is the only evidence.
- Pause length is fixed (no adaptive policy).
- Compared to Coconut and recurrent depth, the latent compute is much shallower (one layer-stack pass vs. recurrent unrolls).

## Trust signals

- **Credibility:** 4 — CMU + Google Research; ICLR 2024 peer-reviewed; no code link in note. Strong venue and groups.

## Follow-up

**Relevance:** 4 — foundational and architecturally minimal. The simplest "buy more latent compute" baseline; project experiments comparing more elaborate continuous-thought architectures should include pause tokens as the cheap baseline to ensure the latent gains aren't just "more compute".
