---
kind: concept
name: "uncertainty trigger"
status: seedling
added: "2026-05-04"
sources: ["literature/papers/lan2026latent.md"]
related_concepts: ["latent-query", "retrieval-as-layer"]
related_experiments: []
tags: ["retrieval", "membrane", "design-move-2"]
---

# Uncertainty trigger

## Definition

A continuous, learned readout from the model's hidden states that decides *when* to perform an external operation (retrieve, call a tool, ask a question) — without first committing the decision to tokens. Replaces the explicit "should I look something up?" reasoning step with a latent-side gate.

## Why it matters here

Direct expression of design-move 2 in the membrane framing. Every token-level commitment is a quantization of an underlying continuous signal; "decide to retrieve" is a particularly wasteful one because it requires verbalizing the decision before acting on it. A learned head over the residual stream is more aligned with the underlying computation.

LAnR is the cleanest existing instance: a lightweight MLP head over the `[PRED]` token's hidden state predicts whether retrieval is sufficient. Empirically, the head tracks answer-token entropy — meaning the model already "knows" how uncertain it is in its activations, and the head just exposes that knowledge as a control signal. No explicit token-level "I should look this up" reasoning is needed.

## Connections

- `latent-query` and `latent-index` — the trigger fires latent retrieval, so it composes naturally with vector queries against a vector index.
- `retrieval-as-layer` — when retrieval lives inside the forward pass, the trigger lives inside the same forward pass and can fire mid-computation.
- **Failure mode:** the trigger predicts entropy, not correctness — confidently wrong answers won't trigger retrieval. A second, complementary signal (calibration, disagreement across paths) may be needed to catch them.
- **Generalization:** the same gating idea applies to deciding when to call a tool, run code, or ask a clarifying question — wherever the current default is "emit a token sequence to commit to the action".
