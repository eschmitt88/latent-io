---
kind: concept
name: "continuous thought"
status: seedling
added: "2026-05-04"
sources: ["literature/papers/hao2024training.md", "literature/papers/geiping2025scaling.md", "literature/papers/goyal2024think.md", "literature/papers/piao2025spiralthinker.md", "literature/papers/zhu2025survey.md", "literature/papers/wang2025system.md", "literature/papers/cheng2024compressed.md", "literature/papers/deng2023implicit.md", "literature/papers/shen2025codi.md", "literature/papers/zhu2025reasoning.md"]
related_concepts: ["commitment-boundary", "uncertainty-trigger"]
related_experiments: []
tags: ["reasoning", "membrane", "core"]
---

# Continuous thought

## Definition

An intermediate representation in the model's residual stream that the model uses for reasoning *without* projecting it through the token vocabulary. Concretely: a hidden state that gets fed back as the next input embedding (Coconut), recurrent-block iteration (Geiping et al.), or a learned latent token slot (pause tokens, contemplation tokens, SpiralThinker's `<latent>` markers).

## Why it matters here

The substrate of all latent cognition in the membrane framing. If tokens are the I/O protocol, continuous thoughts are the actual computation. They matter for two related reasons:

1. **Expressivity.** Continuous thoughts can hold a superposition of alternative next steps — `zhu2025reasoning` proves this formally for graph reachability, and Coconut's probes show it empirically. Discrete tokens commit to a single path at each step and cannot.
2. **Bandwidth.** A token carries one symbol per step; a continuous vector carries hundreds of float-valued dimensions per step. Token CoT bottlenecks the bandwidth of reasoning.

The training-signal question (NOTES.md open #4) is the main obstacle: cross-entropy on next-token is dense and cheap; latent-only training needs auxiliary objectives (alignment in SpiralThinker, distillation in Deng/CODI) or RL (Coconut's curriculum) or just standard LM with recurrent unrolling (Geiping).

## Connections

- `commitment-boundary` — text appears at commitment boundaries; continuous thought is what happens *between* them.
- `uncertainty-trigger` — adaptive depth (Geiping, System-1.5) and adaptive contemplation (CCoT) are uncertainty-driven gating over compute, paralleling the same mechanism applied to retrieval.
- `latent-query` — a latent query is a special case of a continuous thought that gets read out as a retrieval probe.
- **Open question:** continuous thoughts are uninterpretable in the strict sense. Probing (Coconut) and decode-tricks (CLaRa) help but don't fully resolve the debugging problem.
