---
kind: concept
name: "retrieval as a layer"
status: seedling
added: "2026-05-04"
sources: ["literature/papers/he2025bridging.md", "literature/papers/lan2026latent.md", "literature/papers/li2026generation.md", "literature/papers/borgeaud2022improving.md", "literature/papers/izacard2022atlas.md", "literature/papers/khandelwal2020generalization.md", "literature/papers/variengien2025look.md"]
related_concepts: ["latent-query", "latent-index"]
related_experiments: []
tags: ["retrieval", "membrane", "design-move-3"]
---

# Retrieval as a layer

## Definition

Retrieval as an operation embedded *inside* the forward pass of a model — between transformer layers, with a differentiable selection mechanism — rather than an external "turn" in a conversation that gets serialized through tokens, run, and re-ingested.

## Why it matters here

Direct expression of design-move 3 in the membrane framing. If retrieval lives in the forward pass with differentiable selection, two things change:

1. **Composition with cognition.** The model retrieves *during* thinking, not between thoughts — composes naturally with running tools and reading files as latent operations.
2. **Training signal.** Generator gradients can flow back through the retriever, replacing the brittle RL/REINFORCE regimes typical of token-emitted retrieval. CLaRa shows this works via straight-through differentiable top-k.

The technique is not free: differentiable top-k is a relaxation of a discrete operation, and the relaxation has to be tight enough that gradients are informative without collapsing the selection to a soft mixture that doesn't actually retrieve.

## Connections

- `latent-query`, `latent-index` — the two endpoints of the operation this concept describes.
- The mid-layer residual-stream patching results from causal-analysis literature (Universal Emergent Mechanism for Retrieval, ICLR 2025) suggest *where* in the stack retrieval naturally lives — a narrow band of mid-depth layers, not at the input or output.
- **Open question (NOTES.md):** if retrieved facts should *change* the high-level plan, how does the update propagate? Layer-internal retrieval doesn't trivially solve long-horizon coherence.
