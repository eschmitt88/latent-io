---
kind: paper
title: "Genie: Generative Interactive Environments"
authors: ["Jake Bruce", "Michael Dennis", "Ashley Edwards", "Jack Parker-Holder", "Yuge (Jimmy) Shi", "Edward Hughes", "Matthew Lai", "Aditi Mavalankar", "Richie Steigerwald", "Chris Apps", "Yusuf Aytar", "Sarah Bechtle", "Feryal Behbahani", "Stephanie Chan", "Nicolas Heess", "Lucy Gonzalez", "Simon Osindero", "Sherjil Ozair", "Scott Reed", "Jingwei Zhang", "Konrad Zolna", "Jeff Clune", "Nando de Freitas", "Satinder Singh", "Tim Rocktäschel"]
year: 2024
venue: "arXiv (Google DeepMind)"
url: "https://arxiv.org/abs/2402.15391"
source: "raw/papers/bruce2024genie.pdf"
added: "2026-05-04"
relevance: 4
status: skimmed
related_experiments: []
related_concepts: ["action-observation-trace"]
tags: ["foundational", "world-model", "latent-action", "video-pretraining", "deepmind"]
---

# Genie: Generative Interactive Environments

## TL;DR

The first generative interactive environment trained unsupervised on Internet videos. 11B parameters, comprised of a spatiotemporal video tokenizer, autoregressive dynamics model, and a Latent Action Model that infers discrete action labels from frame transitions. Generates action-controllable virtual worlds from text, sketches, photos.

## Claims

- "Action" can be learned as a latent variable from observation transitions alone, without any action labels — Genie's LAM does this from unlabeled video.
- A foundation world model with a latent-action interface enables action-controllable generation across modalities (text → world, sketch → world, photo → world).
- Latent actions are a generalizable interface — they work across game genres, real-world video, and synthetic data.

## Methods

- Spatiotemporal video tokenizer.
- Autoregressive dynamics model: predicts the next visual token sequence given current visual tokens and a latent action.
- Latent Action Model: an inverse-dynamics-style encoder that infers a discrete action token from a pair of consecutive frame embeddings.
- All trained jointly on unlabeled Internet video.

## Results

- 11B parameter model produces interactive, controllable environments.
- Latent actions transfer across content domains (sketches, real-world video).
- Demonstrates an entire foundation-model class — world models — built around the latent-action primitive.

## Critique / open questions

- Discrete (codebook-quantized) latent actions; later work (CLAM, LAOM) argues continuous latents are better for fine-grained motion.
- "Foundation world model" framing is provocative but the model is closer to a foundation video-model with action conditioning than a planning-capable world model.

## Follow-up

**Relevance:** 4 — foundational. Establishes that latent-action interfaces are a viable primitive for world models trained at internet scale. Directly inspires design-move 4 (action–observation traces in latent), and the LAM architecture is the template for thinking about how this project might handle tool-action latents.
