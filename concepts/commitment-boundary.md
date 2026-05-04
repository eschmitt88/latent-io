---
kind: concept
name: "commitment boundary"
status: seedling
added: "2026-05-04"
sources: ["literature/papers/hao2024training.md", "literature/papers/piao2025spiralthinker.md", "literature/papers/cheng2024compressed.md", "literature/papers/geiping2025scaling.md"]
related_concepts: ["continuous-thought"]
related_experiments: []
tags: ["membrane", "core", "tokens-vs-latent"]
---

# Commitment boundary

## Definition

The point at which the model commits its current latent state to a discrete, externally-visible representation (a token, a tool call, a written file, a sent message). Tokens are a *load-bearing* commitment medium because they are what humans, downstream tools, and the next training run will read.

## Why it matters here

The membrane framing is built around the claim that *tokens are load-bearing only at commitment boundaries*. Identifying where the boundaries actually are — and pushing them outward — is the central engineering move of this project.

Examples of boundaries that are real and unavoidable:
- The model's final answer to a user (must be tokens).
- A tool invocation that another process will execute (must be a serializable command).
- An edit applied to a file on disk (must be the literal file contents).

Examples of boundaries that are *currently* token-mediated but don't need to be:
- "Decide to retrieve" (LAnR shows this can be a latent gate, not a token).
- "Generate a search query" (CLaRa shows the query can be a vector, not text).
- "Reason intermediate steps" (Coconut, Geiping, SpiralThinker show these can be latent).

## Connections

- `continuous-thought` — what fills the space between commitment boundaries.
- `uncertainty-trigger` — a latent gate at a commitment boundary; replaces "verbalize the decision" with "predict it from the residual stream."
- `retrieval-as-layer` — when retrieval lives inside the forward pass, the retrieval action is *not* a commitment; only the final answer is.
- **Tension with the inductive-bias hypothesis** (NOTES.md open #5): forcing many small token commitments may be *why* current LLMs generalize OOD. Removing them could make models faster but worse outside training distribution. Speculative; the recurrent-depth result (`geiping2025scaling`) is a counterargument.
