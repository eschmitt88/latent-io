---
kind: moc
name: "membrane"
status: active
added: "2026-08-20"
concepts:
  - "[[concepts/continuous-thought]]"
  - "[[concepts/commitment-boundary]]"
  - "[[concepts/latent-query]]"
  - "[[concepts/latent-index]]"
  - "[[concepts/retrieval-as-layer]]"
  - "[[concepts/uncertainty-trigger]]"
  - "[[concepts/action-observation-trace]]"
tags: ["moc", "membrane", "core"]
---

# Membrane

## The question this theme answers

*Where do tokens actually have to be?*

Current LLM systems do everything interesting in continuous latent space,
but every I/O operation — retrieval, a tool call, reading a file, checking
a test result — forces a hard round-trip through the token vocabulary:
full serialization out, full re-encoding in. The membrane framing holds
that tokens are load-bearing only at *commitment* and *external-tool*
boundaries, and that everywhere else they are scaffolding that costs
bandwidth, differentiability, and expressivity.

These seven concepts belong together because they are the parts of one
argument. Two of them define the substrate and the constraint
(what latent cognition is, and where the token boundary is genuinely
unavoidable). Three describe the first channel we want to push through
the membrane — retrieval — from both endpoints and from the inside of
the forward pass. Two are control and edge: when the membrane opens, and
what a full interaction loop looks like once it does.

## The substrate and the constraint

The pair that frames everything else — one names the medium, the other
names its limit.

- **[[concepts/continuous-thought]]** — the medium. A residual-stream
  representation the model reasons *with* rather than projecting through
  the vocabulary: Coconut's fed-back hidden state, Geiping's recurrent
  depth, SpiralThinker's `<latent>` slots. Its two claims are expressivity
  (a continuous vector can hold a superposition of next steps;
  `[[literature/papers/zhu2025reasoning]]` proves this for graph
  reachability) and bandwidth (hundreds of float dimensions per step
  versus one symbol). Anchored by
  `[[literature/papers/hao2024training]]`,
  `[[literature/papers/geiping2025scaling]]`, and surveyed in
  `[[literature/papers/zhu2025survey]]`.
- **[[concepts/commitment-boundary]]** — the limit. The point where latent
  state must become externally visible: a final answer, a serializable
  tool invocation, literal file contents. The engineering move of this
  project is identifying which boundaries are real and pushing the rest
  outward. `[[literature/papers/cheng2024compressed]]` and
  `[[literature/papers/piao2025spiralthinker]]` mark boundaries that turn
  out to be movable.

## The channel: retrieval without a token round-trip

Design moves 1 and 3. Three concepts describing one operation from its
two endpoints and from inside the stack.

- **[[concepts/latent-query]]** — the query side. The model emits a
  retrieval probe as a vector from its residual stream, eliminating both
  the latent→token projection at emit and the token→latent re-encode at
  lookup, and keeping the operation differentiable.
  `[[literature/papers/he2025bridging]]` (CLaRa) is the concrete
  instantiation; its keyword-decode probe shows the latent query carries
  intermediate-reasoning content a text query would not.
- **[[concepts/latent-index]]** — the corpus side. A pre-encoded store in
  the same space the queries live in, so lookup returns vectors that
  splice straight back into working state. CLaRa's memory tokens are the
  canonical construction; `[[literature/papers/borgeaud2022improving]]`
  (RETRO), `[[literature/papers/izacard2022atlas]]`, and
  `[[literature/papers/khandelwal2020generalization]]` (kNN-LM) are the
  partial prior art this move tries to make *primary* rather than a soft
  assist.
- **[[concepts/retrieval-as-layer]]** — the placement. Retrieval as an
  operation between transformer layers with differentiable selection,
  not a turn in a conversation. This is what lets generator gradients
  flow back into the retriever instead of a brittle REINFORCE regime.
  `[[literature/papers/variengien2025look]]` suggests *where* in the
  stack it belongs — a narrow band of mid-depth layers.

## Control and edge

When the membrane opens, and what the full loop looks like once it does.

- **[[concepts/uncertainty-trigger]]** — design move 2. A learned head
  over hidden states that decides *when* to retrieve, replacing the
  verbalized "should I look this up?" step with a latent gate.
  `[[literature/papers/lan2026latent]]` (LAnR) shows the head tracks
  answer-token entropy — the model already knows how uncertain it is; the
  head just exposes it. Its known failure mode is that entropy is not
  correctness: confidently wrong answers don't fire it.
- **[[concepts/action-observation-trace]]** — design move 4. The full
  interaction shape `(latent_t, action_t, observation_t, latent_{t+1})`,
  where tokens appear *only* at the boundary with the external world and
  cognition on both sides stays continuous. Existing instantiations sit
  at very different points in the design space:
  `[[literature/papers/liu2024deliberation]]` (a computational
  coprocessor returning an injected KV cache),
  `[[literature/papers/bruce2024genie]]` and
  `[[literature/papers/liang2025clam]]` (latent motor actions, next frame
  as observation), and `[[literature/papers/piao2025spiralthinker]]`
  (text steps as the actions between latent iterations).

## Open threads

Two tensions cut across the whole theme and are not resolved by any
concept here.

**Training signal.** Cross-entropy on next-token is dense and cheap;
latent-side cognition needs auxiliary objectives
(`[[literature/papers/piao2025spiralthinker]]`), distillation
(`[[literature/papers/deng2023implicit]]`,
`[[literature/papers/shen2025codi]]`), RL curricula (Coconut), or
recurrent unrolling (`[[literature/papers/geiping2025scaling]]`). For the
tool-use end of the membrane, the latent analogue of Toolformer's
perplexity-reduction signal (`[[literature/papers/schick2023toolformer]]`)
is simply unsolved. `[[literature/papers/nikulin2025latent]]` is the
cautionary result: purely unsupervised latent action learning fails under
distractors.

**The token bottleneck as inductive bias.** The standing hypothesis
against this whole program: forcing many small discrete commitments may
be *why* current LLMs generalize out of distribution, in which case
widening the membrane buys speed and loses robustness. The recurrent-depth
result is the strongest counterargument on hand, and it is not decisive.
Any experiment this MoC leads to should measure OOD behaviour, not just
throughput and in-distribution accuracy.
