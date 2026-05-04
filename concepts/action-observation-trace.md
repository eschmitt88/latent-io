---
kind: concept
name: "action-observation trace"
status: seedling
added: "2026-05-04"
sources: ["literature/papers/liu2024deliberation.md", "literature/papers/bruce2024genie.md", "literature/papers/ye2024latent.md", "literature/papers/liang2025clam.md", "literature/papers/nikulin2025latent.md", "literature/papers/zhang2025what.md", "literature/papers/gao2025adaworld.md", "literature/papers/piao2025spiralthinker.md"]
related_concepts: ["continuous-thought", "commitment-boundary", "latent-query"]
related_experiments: []
tags: ["membrane", "design-move-4", "tool-use", "robotics"]
---

# Action-observation trace

## Definition

A trajectory of the form `(latent_t, action_t, observation_t, latent_{t+1})` where cognition stays continuous and tokens appear *only* at the boundary between the model and the external world. The action is what crosses the membrane outward; the observation is what crosses inward; the latents are the cognition that connects them.

## Why it matters here

Direct expression of design-move 4. A clean story for what tool-use, code execution, and file reading look like under the membrane framing:

- The model's cognition is `latent_t`, a continuous state.
- An action is committed at the boundary — typed appropriately for the external system (a function call, a shell command, a file edit).
- The result returns as an observation — also typed for the external system (text, a number, a structured response).
- The model encodes the action+observation back into `latent_{t+1}` and continues thinking.

Tokens are unavoidable at the boundary, but cognition before and after is continuous.

## Connections

- `commitment-boundary` — the action is the commitment; before and after, latent.
- `continuous-thought` — `latent_t` is a continuous thought; the trace is a sequence of them punctuated by external interactions.
- `latent-query` — retrieval is a special case where the action is "match this query vector" and the observation is "here are the matching vectors."
- `uncertainty-trigger` — decides when to take an action vs. continue thinking in latent. The same gate that triggers retrieval can trigger any tool call.
- **Existing concrete instantiations** at different points in the design space:
  - Liu/Pfeiffer's *Deliberation in Latent Space*: the "tool" is a generic computational coprocessor; observation is an injected KV cache.
  - Genie / LAPA / CLAM: the action is a latent representation of a robotic motor command; observation is the next frame.
  - SpiralThinker: text steps are the "actions" between latent reasoning iterations.
- **Open question (NOTES.md #4):** training signal. Genie/LAPA show unsupervised inverse-dynamics works for vision-action; LAOM shows pure unsupervised fails under distractors. For tool-use, the analog of perplexity-reduction (Toolformer) on the latent side is unsolved.
