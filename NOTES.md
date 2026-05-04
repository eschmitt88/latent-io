# NOTES

Running log of work sessions. `/wrap` appends a new dated section at the
end of each session with **Did / Findings / Next** subsections. The
SessionEnd hook backstops this if you forget.

<!-- entries go below this line, newest at bottom -->

## 2026-05-04 — project framing handoff

### Did

- Scaffolded the project from a multi-session conversation in `/mnt/projects`.
- Settled on display name **Membrane**; folder slug `latent-io` chosen for grep-ability.
- Created private GitHub remote at `eschmitt88/latent-io`.

### Findings (the framing we converged on)

The project studies **model I/O as a selective membrane** between latent
reasoning and the external world (retrieval, code-running, tool use,
filesystem reads, test results). The core observation: current LLM/VLM
systems do everything interesting in continuous latent space, but every
I/O operation forces a hard round-trip through tokens — full
serialization out, full re-encoding in. Tokens are load-bearing at
*commitment* and *external-tool* boundaries; everywhere else they may
be unnecessary scaffolding. The research bet is that pushing the token
boundary outward (to where it's actually needed) buys both efficiency
and capability.

Four design moves we identified, in rough order of ambition:

1. **Latent queries against a latent index.** Model emits a query
   *vector* from its residual stream; corpus is pre-encoded into the
   same space; retrieved vectors splice back into the residual stream
   without a tokenization roundtrip. RETRO/Atlas/kNN-LM are partial
   prior art; the move is to make latent retrieval *primary* rather
   than a soft assist.
2. **Continuous uncertainty as the retrieval trigger.** A learned
   uncertainty head reads the residual stream and fires retrieval when
   above threshold — no token commitment required to "decide to look
   something up." More aligned with how the underlying computation
   actually feels.
3. **Retrieval as a layer, not a turn.** Place retrieval *inside* the
   forward pass between transformer layers. Model retrieves *during*
   thinking, not between thoughts. Composes with running tools and
   reading files as latent operations.
4. **Action–observation traces in latent.** For interactive retrieval
   (running tests, exploring data structures), keep cognition
   continuous and only project to tokens at the boundary with the
   external world. Trace shape: `(latent_t, action_token_t,
   result_token_t, latent_{t+1})`. Tokens are the I/O protocol;
   latents are the cognition.

Adjacent ideas raised earlier in the conversation that *compose* with
this project but aren't its primary axis: scale-conditional projection
(zoom), multi-channel/contrapuntal latent (film as N-channel signal
analogue), and the Plato's-cave framing (tokens as projections of a
richer latent). The membrane framing is the load-bearing one; the
others are useful intuitions to keep in the back pocket.

### Open questions / honest hard problems

- **Embedding compatibility** between a static corpus encoder and a
  live encoder for in-flight artifacts (the file you're editing right
  now). If the encoder drifts during training, the index decays.
- **Latent queries are uninterpretable.** Debugging a wrong-direction
  query is much harder than debugging a wrong text query. May need a
  concurrent token-decode of queries for monitoring.
- **Long-horizon coherence.** When retrieved facts should *change* the
  high-level design, how does the update propagate through a latent
  plan? Token plans propagate via context; latent plans need an
  explicit mechanism. Unsolved.
- **Training signal.** Cross-entropy on next-token is dense and cheap;
  latent-only training needs auxiliary objectives or RL. Engineering
  reason but a real one.
- **Token bottleneck as inductive bias.** Forcing projection through a
  discrete vocabulary may be *why* current LLMs generalize. Removing
  it could make models faster but worse OOD. Speculative.

### Next

1. Re-open Claude Code with cwd inside this project so scoped rules,
   `budget.yaml`, and project `CLAUDE.md` actually load.
2. Fill in the "What this project is about" section of `CLAUDE.md`
   with the membrane framing above (one or two sentences, not the
   essay).
3. Seed `concepts/` with atomic notes for the load-bearing ideas:
   `latent-query.md`, `latent-index.md`, `uncertainty-trigger.md`,
   `retrieval-as-layer.md`, `action-observation-trace.md`,
   `commitment-boundary.md`. Each gets a one-paragraph definition,
   `sources:` (initially empty), and `related_experiments:` (initially
   empty). Wikilinks between them.
4. Use `/discover` to do a first literature sweep on: latent retrieval
   (RETRO, Atlas, kNN-LM), continuous-thought reasoning (Coconut,
   pause tokens), diffusion language models, and tool-use as
   continuous primitives. Drop candidates into `raw/_candidates/`.
5. After ~5 literature notes are ingested, draft a first `/propose`
   for a minimal experiment — likely a latent-query retrieval head
   bolted onto a small open model, evaluated on a code-completion
   task where retrieval matters (e.g. cross-file completion).

The conversation that produced this framing is in the parent dir's
session history; the substance is captured here so future sessions
don't need it.

