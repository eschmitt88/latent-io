---
kind: paper
title: "AdaWorld: Learning Adaptable World Models with Latent Actions"
authors: ["Shenyuan Gao", "Siyuan Zhou", "Yilun Du", "Jun Zhang", "Chuang Gan"]
institutions: ["HKUST", "Harvard University", "UMass Amherst", "MIT-IBM Watson AI Lab"]
year: 2025
venue: "arXiv (HKUST, MIT, U. Mass Amherst)"
peer_reviewed: true
url: "https://arxiv.org/abs/2503.18938"
code_url: "https://adaptable-world-model.github.io"
citations: null
source: "raw/papers/gao2025adaworld.pdf"
added: "2026-05-04"
relevance: 3
credibility: 4
status: skimmed
related_experiments: []
related_concepts: ["action-observation-trace"]
tags: ["world-model", "latent-action", "adaptation", "transfer"]
---

# AdaWorld: Adaptable World Models with Latent Actions

## TL;DR

World-model framework that incorporates *latent action information during pretraining* — extracting actions from videos in a self-supervised manner, capturing the most critical frame-to-frame transitions. The pretrained autoregressive world model conditions on latent actions, enabling efficient transfer and learning of new actions with limited interaction or finetuning. Strong simulation-quality and visual-planning results across multiple environments.

## Claims

- Most existing world models need substantial action-labeled data and don't adapt well; latent-action pretraining gives an embodiment-flexible interface.
- Conditioning the world model on latent actions during pretraining produces a representation that re-grounds across environments and embodiments more easily.
- Latent actions can be re-mapped to new control vocabularies with limited interaction data — the latent is the stable interface, the decoder is environment-specific.

## Methods

- Self-supervised latent action extraction from video frames.
- Autoregressive world model conditioned on latent actions.
- Adaptation: replace or finetune the latent-to-real-action decoder for the new environment.

## Results

- Strong simulation quality and visual planning across multiple environments.
- Efficient transfer to new actions/embodiments.

## Critique / open questions

- "Adaptable" is demonstrated within the simulation-environment family tested; transfer to genuinely different domains (e.g. real-world robotic systems) is a separate harder problem.

## Trust signals

- **Credibility:** 4 — Strong multi-institution (HKUST/Harvard/UMass/MIT-IBM); ICML 2025 (PMLR) peer-reviewed; project page with code/site released.

## Follow-up

**Relevance:** 3 — useful for the long-horizon coherence open question (NOTES.md #3). If latent actions can be re-grounded across environments, that's a candidate mechanism for how an updated retrieval result could re-ground a latent plan. Worth keeping in mind as a structural inspiration.
