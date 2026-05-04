---
kind: paper
title: "Latent Action Pretraining from Videos (LAPA)"
authors: ["Seonghyeon Ye", "Joel Jang", "Byeongguk Jeon", "Sejune Joo", "Jianwei Yang", "Baolin Peng", "Ajay Mandlekar", "Reuben Tan", "Yu-Wei Chao", "Yuchen Lin", "Lars Liden", "Kimin Lee", "Jianfeng Gao", "Luke Zettlemoyer", "Dieter Fox", "Minjoon Seo"]
year: 2024
venue: "ICLR 2025 (KAIST, UW, Microsoft, NVIDIA, AI2)"
url: "https://arxiv.org/abs/2410.11758"
source: "raw/papers/ye2024latent.pdf"
added: "2026-05-04"
relevance: 4
status: skimmed
related_experiments: []
related_concepts: ["action-observation-trace"]
tags: ["latent-action", "vla", "vq-vae", "robot-manipulation", "iclr-2025"]
---

# LAPA: Latent Action Pretraining from Videos

## TL;DR

First unsupervised method for pretraining Vision-Language-Action models *without* ground-truth robot action labels. Three stages: (1) train a VQ-VAE to learn discrete latent actions between image frames; (2) pretrain a latent VLA to predict latent actions from observations and task descriptions; (3) finetune on small-scale robot manipulation data to map latent → robot actions. Outperforms VLAs trained on hundreds of thousands of labeled robot actions, especially on transfer to unseen tasks/instructions/embodiments.

## Claims

- Action labels are the bottleneck for VLA pretraining; unsupervised latent-action pretraining bypasses it.
- Latent actions learned from internet-scale videos transfer to physical robotic embodiments with only modest finetuning data.
- The same latent-action vocabulary works across embodiments — i.e. embodiment-specific decoding sits at the boundary, with cognition kept embodiment-general.

## Methods

- Stage 1: VQ-VAE on (frame, next-frame) pairs → discrete latent action codes.
- Stage 2: VLA backbone trained to predict latent actions given observations + task descriptions.
- Stage 3: small finetune on labeled robot data; learns latent → real-action decoder.

## Results

- Outperforms VLAs trained on much larger labeled datasets, especially OOD.
- Strongest gains on transfer to unseen tasks/instructions/embodiments.

## Critique / open questions

- VQ-VAE quantization is the design choice CLAM and LAOM later argue against; LAPA inherits the codebook-collapse and granularity-mismatch issues that come with discrete latents.
- "Latent action" is action-relevant change in observation space; if observation contains distractors (LAOM's concern), the latent is contaminated.

## Follow-up

**Relevance:** 4 — direct application of design-move 4 in a different domain (robotics). Demonstrates the architecture works at scale and is the template for the project's bet that latent action representations transfer.
