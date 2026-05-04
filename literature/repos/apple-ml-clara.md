---
kind: repo
name: "apple/ml-clara"
authors: ["Apple"]
year: 2025
venue: "GitHub"
url: "https://github.com/apple/ml-clara"
source: "raw/repos/apple-ml-clara.md"
added: "2026-05-04"
relevance: 4
status: skimmed
related_experiments: []
related_concepts: ["latent-query", "latent-index", "retrieval-as-layer"]
tags: ["implementation", "reference-code", "huggingface-models"]
---

# apple/ml-clara

## TL;DR

Official open-source release of CLaRa (`he2025bridging`) — Apple's continuous-latent RAG model. Includes three checkpoint variants (Base, Instruct, E2E) on Hugging Face, multi-stage training datasets, and evaluation data; License is Apple's permissive.

## Notes

- Three-stage training pipeline matches the paper's narrative: compression pretraining → compression instruction tuning → end-to-end fine-tuning.
- 32×–64× compression rates (README claims) — slightly more aggressive than the 16× quoted in the paper abstract.
- MLX version was in progress as of Dec 2025; useful for local inference on Apple Silicon.

## Follow-up

**Relevance:** 4 — direct reference implementation for the load-bearing paper. Read the code before scoping the first project experiment.
