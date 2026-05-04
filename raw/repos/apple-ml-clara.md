---
kind: repo
source_url: https://github.com/apple/ml-clara
fetched: 2026-05-04
title: "apple/ml-clara — Official CLaRa implementation"
---

# apple/ml-clara

Reference implementation for CLaRa (literature/papers/he2025bridging.md). State-of-the-art end-to-end RAG model, three-stage training (compression pretraining → compression instruction tuning → end-to-end fine-tuning).

## Key resources

- Paper: arXiv:2511.18659
- Models on Hugging Face:
  - apple/CLaRa-7B-Base
  - apple/CLaRa-7B-Instruct
  - apple/CLaRa-7B-E2E
- Dataset: apple/CLaRa_multi_stage (multi-stage training data)
- Evaluation data: `./evaluation/evaluation_data` in the repo
- License: Apple

## Notable findings called out by the README

- **Efficient compression**: 32×–64× compression rates while preserving QA accuracy.
- **Three-stage training**: compression pretraining + compression instruction tuning + end-to-end fine-tuning.
- An MLX version is announced as "in progress" (per README, Dec 10, 2025 update).

## Why fetch this

- Concrete starting point for the first proposed experiment in NOTES.md (latent-query retrieval head bolted onto a small open model).
- Reading the implementation will clarify engineering details — gradient routing through the differentiable top-k, encoder choice, LoRA-adapter wiring — that the paper glosses.
