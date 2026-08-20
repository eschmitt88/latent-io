---
kind: candidates
topic: "continuous-thought reasoning (Coconut, pause tokens)"
discovered: 2026-05-04
source: discover
curated: 2026-08-20
n_requested: 10
n_returned: 10
---

# Continuous-thought reasoning — triage 2026-05-04

Ranked by relevance to the membrane framing — specifically, the claim
that latent space is the right substrate for *cognition* and tokens are
only the I/O protocol. Direct hits first; foundational priors next;
analyses and surveys at the bottom.

## 1. Coconut: Training Large Language Models to Reason in a Continuous Latent Space

- url: https://arxiv.org/abs/2412.06769
- type: paper
- summary: Hao et al. (Meta) feed the model's last-layer hidden state directly back as the next input embedding instead of decoding to text — "continuous thoughts" that can encode multiple alternative next steps, enabling latent BFS on logical reasoning tasks.
- reason: Named prior and the cleanest experimental demonstration of the project's central thesis: latent reasoning is not just an efficiency trick, it can encode superpositions that token-CoT cannot. Code at github.com/facebookresearch/coconut.

## 2. Scaling up Test-Time Compute with Latent Reasoning: A Recurrent Depth Approach

- url: https://arxiv.org/abs/2502.05171
- type: paper
- summary: Geiping et al. train a 3.5B model with a recurrent transformer block that can be unrolled to arbitrary depth at test time, scaling reasoning compute *vertically* in latent space instead of horizontally in tokens; matches CoT-style gains on math and code with no specialized data, no special context window. NeurIPS 2025 spotlight.
- reason: The most ambitious "all cognition in latent" demonstration available — it doesn't even need supervised reasoning traces. Direct precedent for the project's idea that latent compute should be the default and tokens the boundary protocol. Argues against the inductive-bias counterargument in NOTES.md by showing strong reasoning emerges without token-mediated supervision.

## 3. Think before you speak: Training Language Models With Pause Tokens

- url: https://arxiv.org/abs/2310.02226
- type: paper
- summary: Goyal et al. (ICLR 2024) introduce a learnable pause token; appending pauses to the prefix delays output and lets the model use extra hidden-state computation before committing — works best when used during both pretraining and fine-tuning.
- reason: Named prior. The simplest possible "buy more latent compute" move, and the cleanest baseline to compare more elaborate continuous-thought architectures against. Useful when scoping the first experiment in NOTES.md to ensure gains are not just "more compute".

## 4. SpiralThinker: Latent Reasoning through Iterative Text–Latent Interleaving

- url: https://arxiv.org/abs/2511.08983
- type: paper
- summary: Frames latent reasoning as an iterative process: prepend N latent tokens, run them through the model, generate explicit textual steps, then autonomously insert more latent tokens after each text step, alternating implicit/explicit reasoning until termination. SOTA on GSM8K-Aug, ProsQA, StrategyQA among latent methods.
- reason: Most directly relevant to the membrane framing — explicit text appears only at "commitment boundaries" while cognition happens in latent. The training scheme (alternating modes) is a candidate template for action–observation traces (design-move 4).

## 5. A Survey on Latent Reasoning

- url: https://arxiv.org/abs/2507.06203
- type: paper
- summary: Comprehensive 2025 survey covering continuous CoT, recurrent-depth, implicit reasoning, and latent compression — argues that token-level CoT bottlenecks expressive bandwidth and that latent reasoning eliminates that bottleneck.
- reason: Field-orienting reference. Read once early to identify prior art the discover sweep missed, then keep as the standing index when seeding `concepts/`. The companion repo (multimodal-art-projection/LatentCoT-Horizon) is a curated paper list.

## 6. System-1.5 Reasoning: Traversal in Language and Latent Spaces with Dynamic Shortcuts

- url: https://arxiv.org/abs/2505.18962
- type: paper
- summary: NeurIPS 2025 framework that distills text CoT into continuous thought, then distills full-path latent reasoning into two kinds of dynamic shortcuts (depth shortcut: skip layers for non-critical tokens; step shortcut: reuse hidden states across decoding steps); 20× speedup, 91% token reduction on GSM8K.
- reason: Practical exemplar of "compute belongs where the cognition is dense, tokens belong only at commitment." The two-stage distillation is directly applicable if the project wants to bootstrap from existing CoT-trained models rather than train from scratch.

## 7. Compressed Chain of Thought (CCoT): Efficient Reasoning through Dense Representations

- url: https://arxiv.org/html/2412.13171v1
- type: paper
- summary: Generates contemplation tokens that are continuous-valued compressed representations of an explicit reasoning chain, used in place of textual CoT for efficient inference.
- reason: A complementary architectural sketch for the latent–token boundary: instead of replacing tokens entirely (Coconut), produce continuous "summary" tokens. Useful contrast for the project's design space when picking the right level of latent commitment.

## 8. Implicit Chain of Thought Reasoning via Knowledge Distillation

- url: https://arxiv.org/abs/2311.01460
- type: paper
- summary: Deng et al. distill explicit-CoT teacher hidden states into a student model so the student reasons "vertically" through layers without producing intermediate text — does reasoning across layers instead of across tokens.
- reason: The original "no-tokens" implicit-CoT formulation. Useful as a historical baseline and because the cross-layer reasoning view connects naturally to design-move 3 (retrieval as a layer): if reasoning lives in layers, retrieval should too.

## 9. CODI: Compressing Chain-of-Thought into Continuous Space via Self-Distillation

- url: https://aclanthology.org/2025.emnlp-main.36.pdf
- type: paper
- summary: Self-distillation framework that jointly learns explicit and implicit reasoning traces, compressing CoT into continuous representations without a separate teacher. EMNLP 2025.
- reason: The self-distillation formulation removes the dependence on a strong teacher, which matters for the project's compute budget. Useful methods reference for the first proposed experiment.

## 10. Reasoning by Superposition: A Theoretical Perspective on Chain of Continuous Thought

- url: https://arxiv.org/abs/2505.12514
- type: paper
- summary: Theoretical analysis arguing that Coconut-style continuous thoughts implement a form of superposition over reasoning paths, providing the formal grounding for why latent BFS outperforms greedy token CoT on planning tasks.
- reason: Theoretical anchor for the load-bearing claim that latent representations have computational properties tokens don't. Important for writing the project's `concepts/latent-query.md` and `commitment-boundary.md` notes with grounded claims rather than intuitions.

## Curation

Curated 2026-08-20. All ten entries were already resolved into the graph by
the ingest pass that followed `/discover`.

1. Coconut — already in graph → `hao2024training`
2. Recurrent-depth latent reasoning — already in graph → `geiping2025scaling`
3. Pause tokens — already in graph → `goyal2024think`
4. SpiralThinker — already in graph → `piao2025spiralthinker`
5. A Survey on Latent Reasoning — already in graph → `zhu2025survey`
6. System-1.5 Reasoning — already in graph → `wang2025system`
7. Compressed Chain of Thought — already in graph → `cheng2024compressed`
8. Implicit CoT via Knowledge Distillation — already in graph → `deng2023implicit`
9. CODI — already in graph → `shen2025codi`
10. Reasoning by Superposition — already in graph → `zhu2025reasoning`

ingested=0 declined=0 dup=10
