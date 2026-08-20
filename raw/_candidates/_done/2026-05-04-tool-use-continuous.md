---
kind: candidates
topic: "tool-use as continuous primitives"
discovered: 2026-05-04
source: discover
curated: 2026-08-20
n_requested: 10
n_returned: 10
---

# Tool use as continuous primitives — triage 2026-05-04

Ranked by relevance to design-move 4 in NOTES.md (action–observation
traces in latent, with tokens only at the external boundary). Two
threads matter: (a) latent-action models (LAMs) treating control as a
continuous primitive, and (b) latent-side LM augmentations that
substitute for explicit tool tokens. Direct hits first; the LAM
literature next; named priors and surveys at the bottom.

## 1. Deliberation in Latent Space via Differentiable Cache Augmentation

- url: https://arxiv.org/abs/2412.17747
- type: paper
- summary: Google DeepMind augments a frozen LLM with an offline "coprocessor" that operates on the kv-cache, injecting latent embeddings learned end-to-end via the standard LM loss; works asynchronously, the decoder remains usable without it, and it consistently reduces perplexity and improves reasoning-task performance with no task-specific training.
- reason: The closest existing work to "tool use as a continuous primitive in the project's exact sense — the 'tool' is a learned latent computation that injects into the model's working state without ever being verbalized as a token. End-to-end differentiable, asynchronous, and falls back gracefully — directly templates how the project should structure latent tool calls.

## 2. Genie: Generative Interactive Environments

- url: https://arxiv.org/abs/2402.15391
- type: paper
- summary: DeepMind's 11B foundation model trained unsupervised on Internet video, with a spatiotemporal video tokenizer, autoregressive dynamics model, and a Latent Action Model that infers discrete latent actions from frame transitions — turning unlabeled video into a controllable interactive environment.
- reason: The foundational demonstration that "control" can be learned as a latent variable from observation streams alone, without action labels. Directly motivates treating tool invocations as latent primitives inferred from action–observation pairs (design-move 4).

## 3. Latent Action Pretraining from Videos (LAPA)

- url: https://arxiv.org/abs/2410.11758
- type: paper
- summary: Pretrains a vision-language-action model with latent actions inferred from unlabeled video; matches or exceeds policies trained on hundreds of thousands of labeled robot actions, especially on transfer to unseen tasks, instructions, or embodiments.
- reason: Directly tests the project's hypothesis at scale in a different domain — that latent action representations learned without language supervision can serve as the cognition substrate, with text only at the boundary. Useful prior art when arguing the latent-action interface generalizes.

## 4. CLAM: Continuous Latent Action Models for Robot Learning

- url: https://liralab.usc.edu/pdfs/publications/liang2025clam.pdf
- type: paper
- summary: USC's Continuous Latent Action Models drop the discrete action codebook used in Genie/LAPA-style LAMs in favor of continuous latents, supporting more expressive action spaces and finer transfer to novel tasks.
- reason: Most direct demonstration that continuous (not quantized) latent actions are not just feasible but better — relevant evidence for the project's bet that the right representation at the membrane is continuous, not a discrete bottleneck.

## 5. Latent Action Learning Requires Supervision in the Presence of Distractors (LAOM)

- url: https://arxiv.org/abs/2502.00379
- type: paper
- summary: Nikulin et al. (ICML 2025) propose multi-step inverse dynamics, drop codebook quantization for high-capacity continuous latents, and show that a small fraction (~2.5%) of ground-truth action supervision improves downstream performance 4.2× when distractors are present in observation streams.
- reason: Honest negative finding the project should heed: pure unsupervised latent action learning fails when the observation stream contains distractors. Directly relevant to the project's open question about training signal — argues for hybrid supervised/self-supervised regimes rather than fully unsupervised latent objectives.

## 6. Toolformer: Language Models Can Teach Themselves to Use Tools

- url: https://arxiv.org/abs/2302.04761
- type: paper
- summary: Schick et al. self-supervise tool use by inserting candidate API calls into pretraining text and keeping only those that reduce perplexity on subsequent tokens; the model autonomously decides when and what to call without human annotation.
- reason: The reference point for the *token-emitted* tool-use regime that this project is arguing against. Reading it carefully clarifies what is hard about pulling tool-use into latent: the perplexity-reduction signal is what makes Toolformer's self-supervision work, and any latent-tool variant needs an analogous training signal.

## 7. What Do Latent Action Models Actually Learn?

- url: https://arxiv.org/abs/2506.15691
- type: paper
- summary: Empirical analysis of what LAM latent codes actually represent across multiple training regimes — disentangling agent-driven dynamics from environmental and appearance variation, and probing whether the latents support transfer.
- reason: Directly relevant to the "latent queries are uninterpretable" open question in NOTES.md. If we are going to make latent actions a primary primitive, we need diagnostics for what they encode — this paper's probes are a good starting template.

## 8. AdaWorld: Learning Adaptable World Models with Latent Actions

- url: https://arxiv.org/abs/2503.18938
- type: paper
- summary: World-model framework where latent actions serve as the action interface; adapts to new environments and tasks by re-grounding the same latent action vocabulary, supporting cross-environment transfer.
- reason: Useful for the long-horizon-coherence open question — if latent actions can be re-grounded across environments, that's a path to making latent plans coherent under changing context. A specific candidate mechanism for "how does an update propagate through a latent plan."

## 9. Tool learning with language models: a comprehensive survey

- url: https://link.springer.com/article/10.1007/s44336-025-00024-x
- type: paper
- summary: 2025 survey of tool-use methods, pipelines, and benchmarks for LLMs — covers retrieval-based tool selection, function-calling regimes, planning, and chain-of-tools.
- reason: Field-orienting reference for the *token-emitted* end of the spectrum. Read once to identify what existing tool-use benchmarks exist that a latent-tool architecture could be evaluated on.

## 10. Efficient Vision-Language-Action Models for Embodied Manipulation: A Systematic Survey

- url: https://arxiv.org/html/2510.17111v1
- type: paper
- summary: Recent VLA survey covering how vision-language-action backbones incorporate latent actions as bottleneck/mid-level interface layers, latent action queries, and the diffusion-based action heads commonly bolted on top.
- reason: The most relevant survey for understanding architectural patterns at the latent-action / token boundary. Directly informs the question of *where* in the model the latent–token transition should sit, which is the membrane in design-move 4.

## Curation

Curated 2026-08-20. Nine of ten entries were already resolved into the graph
by the ingest pass that followed `/discover`; the tenth is declined.

1. Differentiable Cache Augmentation — already in graph → `liu2024deliberation`
2. Genie — already in graph → `bruce2024genie`
3. LAPA — already in graph → `ye2024latent`
4. CLAM — already in graph → `liang2025clam`
5. LAOM — already in graph → `nikulin2025latent`
6. Toolformer — already in graph → `schick2023toolformer`
7. What Do Latent Action Models Actually Learn? — already in graph → `zhang2025what`
8. AdaWorld — already in graph → `gao2025adaworld`
9. Tool learning with language models (survey) — **declined** — full text is
   not retrievable (Springer serves a bot challenge; no open-access PDF or
   arXiv mirror), so `/fetch-paper` cannot produce a usable artifact. The
   token-emitted end of the tool-use spectrum is already anchored by
   `schick2023toolformer` (the reference regime) and `guan2025efficient`
   (architectural patterns at the latent–token boundary), so the marginal
   value of a paywalled survey is low. Revisit only if a benchmark survey
   becomes load-bearing for an experiment.
10. Efficient VLA Models (survey) — already in graph → `guan2025efficient`

ingested=0 declined=1 dup=9
