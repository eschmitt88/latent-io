---
kind: concept
name: "latent index"
status: seedling
added: "2026-05-04"
sources: ["literature/papers/he2025bridging.md", "literature/papers/lan2026latent.md", "literature/papers/khandelwal2020generalization.md", "literature/papers/wei2025mlp.md", "literature/papers/izacard2022atlas.md", "literature/papers/borgeaud2022improving.md", "literature/papers/zhang2025memory.md"]
related_concepts: ["latent-query", "retrieval-as-layer"]
related_experiments: []
tags: ["retrieval", "membrane", "design-move-1"]
---

# Latent index

## Definition

A pre-encoded corpus stored as continuous vectors in the same representational space the model emits queries from. Lookup yields vectors that splice back into the model's working state directly, without any tokenization step on either the query or the result side.

## Why it matters here

The corpus side of design-move 1 (paired with `latent-query`). Together they form the membrane: a high-bandwidth, differentiable channel between cognition (latent) and stored knowledge (latent), reserving tokens for external commitment.

CLaRa's "memory tokens" are the canonical construction so far: each document gets `l` learnable memory tokens appended; the compressor LoRA produces a fixed-size representation from their final-layer hidden states. The same encoding serves *both* retrieval (as the searchable representation) and generation (as the input to the answer-producing head) — eliminating the architectural mismatch where retrievers think in vectors but generators consume text.

## Connections

- `latent-query` — the query side of the same operation.
- `retrieval-as-layer` — a latent index is the precondition for retrieval-inside-the-forward-pass.
- **Open question (NOTES.md #1):** embedding compatibility between a static index encoder and a live encoder for in-flight artifacts is unsolved. CLaRa side-steps it by sharing base weights between compressor and generator; a project that wants live encoding (e.g. the file you're editing) needs a different answer.
- **Compression vs. fidelity tradeoff:** memory-token count `l` is the explicit knob — too small loses information, too large defeats the efficiency motivation. CLaRa reports 16× as a sweet spot; the failure modes above and below are uncharted.
