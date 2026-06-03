---
kind: paper
title: "CLAM: Continuous Latent Action Models for Robot Learning from Unlabeled Demonstrations"
authors: ["Anthony Liang", "Pavel Czempin", "Matthew Hong", "Yutai Zhou", "Erdem Bıyık", "Stephen Tu"]
institutions: ["University of Southern California (CS and ECE Departments)"]
year: 2025
venue: "Liralab USC"
peer_reviewed: unknown
url: "https://liralab.usc.edu/pdfs/publications/liang2025clam.pdf"
code_url: "https://clamrobot.github.io"
citations: null
source: "raw/papers/liang2025clam.pdf"
added: "2026-05-04"
relevance: 4
credibility: 3
status: skimmed
related_experiments: []
related_concepts: ["action-observation-trace"]
tags: ["latent-action", "continuous-actions", "robot-learning", "fine-grained-control"]
---

# CLAM: Continuous Latent Action Models

## TL;DR

CLAM identifies two fixes that make latent-action models work for *fine-grained* robot tasks where prior LAM/LAPA-style methods struggle: (a) use *continuous* latent actions instead of discrete (VQ codebook) representations, (b) jointly train an action decoder so the latent space is grounded with relatively few labeled examples. Crucially, the labeled examples can be non-optimal play data — no expert demonstrations needed.

## Claims

- Discrete latent actions (codebook quantization) lose the fine-grained motion structure that complex continuous control tasks require.
- Joint training of the latent action encoder and a real-action decoder — even with very few labels — is what makes the latent space *useful*, not just learnable.
- "Useful labels" can be *non-optimal* — play data, not expert demonstrations. This dramatically lowers the labeling burden.

## Methods

- Continuous latent action representation (no codebook).
- Joint training: latent action encoder + decoder to ground actions, on a mix of unlabeled video (most of the data) and small labeled play-data examples.

## Results

- CLAM solves complex continuous-control tasks where prior LAMs fail.
- Performance scales with unlabeled data; small label budget suffices.

## Critique / open questions

- "Fine-grained continuous control" is the regime CLAM was designed for; CLAM's advantage over discrete LAMs on simple discrete-action tasks is less clear.
- Joint training requires *some* labels; truly label-free latent-action pretraining (Genie's claim) is a separate goal.

## Trust signals

- **Credibility:** 3 — USC robotics group; venue peer-review status unclear from source; code + videos released (clamrobot.github.io). Reproducibility partly offsets unknown venue.

## Follow-up

**Relevance:** 4 — the cleanest argument that latent actions for control should be *continuous*, not discretely quantized. Directly informs the project's bet that the right representation at the membrane is continuous, not codebook-quantized.
