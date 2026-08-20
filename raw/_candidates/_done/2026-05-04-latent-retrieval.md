---
kind: candidates
topic: "latent retrieval (RETRO, Atlas, kNN-LM)"
discovered: 2026-05-04
source: discover
curated: 2026-08-20
n_requested: 10
n_returned: 10
---

# Latent retrieval — triage 2026-05-04

Ranked by fit to the membrane framing (latent queries against a latent
index, retrieval as a layer rather than a turn). Top entries are recent
direct hits; named priors (RETRO, Atlas, kNN-LM) sit in the middle as
required reading. Bottom entries broaden the field of view.

## 1. CLaRa: Bridging Retrieval and Generation with Continuous Latent Reasoning

- url: https://arxiv.org/abs/2511.18659
- type: paper
- summary: Apple research framework that compresses documents to a shared continuous space and trains reranker + generator end-to-end with a differentiable top-k estimator and a single LM loss; achieves 16–128× compression while beating text-based fine-tuned baselines on QA.
- reason: Closest existing work to design-move 1 (latent queries against a latent index) — joint training in shared continuous space with gradients flowing through retrieval is exactly the architecture the project is betting on. Code at github.com/apple/ml-clara makes this implementable.

## 2. Latent Abstraction for Retrieval-Augmented Generation (LAnR)

- url: https://arxiv.org/abs/2604.17866
- type: paper
- summary: Single LLM performs encoding, retrieval, and generation entirely in its own latent space — generates dense query vectors from the hidden states of a designated [PRED] token and uses an MLP control head that decides when to stop retrieving based on answer-token entropy.
- reason: Directly fuses design-moves 1 (latent queries) and 2 (continuous uncertainty as retrieval trigger) — the entropy-monitor MLP is essentially the "uncertainty head" the membrane framing posits. April 2026, very recent.

## 3. Generation-Augmented Generation (GAG): Plug-and-Play Latent Knowledge Injection

- url: https://arxiv.org/html/2601.08209
- type: paper
- summary: Distills question-conditioned knowledge from lightweight domain experts into multi-slot latent memories and injects them into a frozen base model through gated residual projection, with no base-model parameter updates.
- reason: The clearest worked example of design-move 3 — retrieval as a layer via residual-stream injection, constant-budget latent interface. Useful as a concrete architecture to compare against and a reference for how to keep the base model frozen.

## 4. Improving Language Models by Retrieving from Trillions of Tokens (RETRO)

- url: https://arxiv.org/abs/2112.04426
- type: paper
- summary: DeepMind's chunked cross-attention retrieval-augmented decoder retrieves k neighbours of r tokens for each chunk and integrates them with linear time complexity in retrieved data; matches GPT-3 with 25× fewer parameters when paired with a 2T-token retrieval database.
- reason: Named prior. Foundational for "retrieval as a layer" — chunked cross-attention is a token-level version of what design-move 3 wants in latent. Required reading for any serious latent-retrieval architecture proposal.

## 5. Atlas: Few-shot Learning with Retrieval Augmented Language Models

- url: https://arxiv.org/abs/2208.03299
- type: paper
- summary: Encoder-decoder LM jointly trained with a retriever, modeling retrieved documents as latent variables; achieves competitive few-shot performance on QA and fact-checking with 50× fewer parameters than larger models.
- reason: Named prior. The "documents as latent variables" framing is the philosophical ancestor of treating retrieval as latent-space operations rather than text concatenation. Joint retriever-LM training is the regime the project will inherit.

## 6. Generalization through Memorization: Nearest Neighbor Language Models (kNN-LM)

- url: https://arxiv.org/abs/1911.00172
- type: paper
- summary: Augments a pretrained LM by linearly interpolating its next-token distribution with a kNN distribution computed over neighbours retrieved (in the LM's own embedding space) from a datastore; SOTA Wikitext-103 perplexity 15.79 with no additional training.
- reason: Named prior. The original "retrieve in LM embedding space" move — the simplest architectural ancestor of latent retrieval. Architecturally trivial, which makes it a useful baseline and a useful sanity check on whether "latent" is doing real work.

## 7. MLP Memory: Language Modeling with Retriever-pretrained External Memory

- url: https://arxiv.org/abs/2508.01832
- type: paper
- summary: Replaces kNN-LM's vector datastore with a fully parameterized MLP that is pretrained to imitate retriever behavior over the entire pretraining corpus; 80× faster inference, 220 GB → 2.8 GB storage, fully differentiable end-to-end.
- reason: An interesting alternative answer to "where does the latent index live" — instead of a vector store, bake the retriever into parameters. Worth considering as the contrast point to a fully external latent index, especially for the embedding-compatibility open question in NOTES.md.

## 8. Universal Emergent Mechanism for Retrieval

- url: https://proceedings.iclr.cc/paper_files/paper/2025/file/ad36c2cfc423e75c6d68d751a955b22e-Paper-Conference.pdf
- type: paper
- summary: ICLR 2025 causal analysis across 18 open-source LMs (125M–70B) showing that retrieval-task behavior can be patched at a narrow band of mid-layer residual-stream sites, supporting a layer-localized view of in-context retrieval.
- reason: Empirical grounding for design-move 3 — if real retrieval-relevant computation already concentrates in a narrow mid-layer band, that's the natural site to splice an external latent index into the residual stream. Tells the project where to inject.

## 9. apple/ml-clara (reference implementation)

- url: https://github.com/apple/ml-clara
- type: repo
- summary: Official codebase for CLaRa (entry #1) — Apple's continuous-latent reasoning framework with differentiable top-k retrieval and joint reranker/generator training.
- reason: Concrete starting point for the first experiment proposed in NOTES.md (latent-query retrieval head bolted onto a small open model). Reading the implementation will surface engineering details (gradient routing through top-k, encoder choice) that the paper glosses.

## 10. Memory in Large Language Models: Mechanisms, Evaluation and Evolution (survey)

- url: https://arxiv.org/pdf/2509.18868
- type: paper
- summary: Recent survey covering parametric memory, in-context memory, and retrieval-augmented memory across LLMs; includes evaluation protocols and evolution of memory architectures.
- reason: Cheap orientation read to surface prior art the discover sweep missed (especially around long-term and episodic-memory variants). Useful for building the concept-graph rather than for direct experimental reference.

## Curation

Curated 2026-08-20. Every entry in this file was already resolved into the
graph by the ingest pass that followed `/discover`; nothing new to fetch.

1. CLaRa — already in graph → `he2025bridging`
2. LAnR — already in graph → `lan2026latent`
3. GAG — already in graph → `li2026generation`
4. RETRO — already in graph → `borgeaud2022improving`
5. Atlas — already in graph → `izacard2022atlas`
6. kNN-LM — already in graph → `khandelwal2020generalization`
7. MLP Memory — already in graph → `wei2025mlp`
8. Universal Emergent Mechanism for Retrieval — already in graph → `variengien2025look`
9. apple/ml-clara — already in graph → `literature/repos/apple-ml-clara.md`
10. Memory in LLMs (survey) — already in graph → `zhang2025memory`

ingested=0 declined=0 dup=10
