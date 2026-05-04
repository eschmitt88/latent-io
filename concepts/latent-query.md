---
kind: concept
name: "latent query"
status: seedling
added: "2026-05-04"
sources: ["literature/papers/he2025bridging.md", "literature/papers/lan2026latent.md"]
related_concepts: ["latent-index", "retrieval-as-layer"]
related_experiments: []
tags: ["retrieval", "membrane", "design-move-1"]
---

# Latent query

## Definition

A query against an external store that the model emits as a continuous vector (typically derived from a hidden state or a designated query token), rather than as a sequence of text tokens that must then be re-encoded. The store returns vectors back into the model's working state without a tokenization round-trip.

## Why it matters here

Direct expression of design-move 1 in the membrane framing: tokens are load-bearing only at *commitment* and *external-tool* boundaries, and a retrieval lookup doesn't need to cross either. Pushing the query out as a vector eliminates two unnecessary projections (latent → token at emit, token → latent at retrieve), and — critically — keeps the operation differentiable end-to-end.

The CLaRa paper provides a concrete instantiation: a "query reasoner" produces an embedding, which selects compressed document vectors via differentiable top-k. A keyword-decode probe of the latent query reveals it contains intermediate-reasoning content not present in the original question — early evidence that the latent query is *doing more work* than a token query would.

## Connections

- `latent-index` — the corpus side of the same operation. Latent queries are useless without a compatible vector store.
- `retrieval-as-layer` — when the retrieval step is differentiable and lives inside the forward pass, it stops being a "turn" in a conversation and becomes a layer.
- The "latent queries are uninterpretable" open question in NOTES.md is real but partly addressable via decode-probes (CLaRa Fig 1b).
