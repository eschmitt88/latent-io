---
kind: paper
title: "CLaRa: Bridging Retrieval and Generation with Continuous Latent Reasoning"
authors: ["Jie He", "Richard He Bai", "Sinead Williamson", "Jeff Z. Pan", "Navdeep Jaitly", "Yizhe Zhang"]
institutions: ["Apple", "University of Edinburgh"]
year: 2025
venue: "arXiv (Apple, U. Edinburgh)"
peer_reviewed: false
url: "https://arxiv.org/abs/2511.18659"
code_url: "https://github.com/apple/ml-clara"
citations: null
source: "raw/papers/he2025bridging.pdf"
added: "2026-05-04"
relevance: 5
credibility: 4
status: skimmed
related_experiments: []
related_concepts: ["latent-query", "latent-index", "retrieval-as-layer"]
tags: ["latent-retrieval", "rag", "differentiable-top-k", "compression", "joint-training"]
---

# CLaRa: Bridging Retrieval and Generation with Continuous Latent Reasoning

## TL;DR

A unified RAG framework where documents are encoded once into a compact set of "memory tokens" that simultaneously serve retrieval and generation in a shared continuous space; the reranker and generator train end-to-end via a single LM loss with gradients flowing through a differentiable top-k via straight-through estimation. Achieves SOTA QA performance even at 16× text compression, beating text-based fine-tuned baselines.

## Claims

- Conventional RAG suffers from two structural defects: (i) retrievers operate in embedding space while generators consume raw text, blocking end-to-end optimization, and (ii) discrete document selection prevents gradient flow from generator back to retriever — the project should treat both as load-bearing diagnoses.
- Continuous, compact document representations + joint optimization are inherently complementary: continuous encodings make retrieval differentiable; joint training aligns retriever and generator in the same semantic space.
- A salient-info–aware pretraining objective (SCP) outperforms token-level reconstruction at producing retrievable compressed vectors — bottlenecks built around QA / paraphrase signals beat bottlenecks built around byte-level fidelity.
- End-to-end joint training with straight-through differentiable top-k can replace the typical RL/REINFORCE-style retriever update.

## Methods

- **Stage I — SCP (Salient Compressor Pretraining).** Synthesize 2M Wikipedia-derived training items via a Qwen-32B teacher: simple QA, complex QA, and paraphrases, with iterative coverage verification. Train a shared base LLM with two LoRA adapters (compressor + generator). Documents get `l` appended learnable memory tokens; the compressor LoRA produces `M_i` from the final-layer hidden states of those memory tokens; only the generator LoRA is trained on cross-entropy + an MSE alignment loss between mean memory-token hidden state and mean document-token hidden state.
- **Stage II — End-to-end joint training.** A "query reasoner" produces a query embedding; differentiable top-k via straight-through estimation selects compressed document representations; reasoner + generator update under a single next-token-prediction loss. Theoretical claim: this unified objective yields valid retriever gradients without explicit retrieval labels.
- Backbones: Mistral-7B and Phi-4B. Eval on four single-hop and multi-hop QA benchmarks.

## Results

- SOTA retrieval and generation performance against supervised and unsupervised baselines.
- Surpasses text-only DRO methods at a 16× text compression ratio — i.e. the latent compression doesn't trade quality for compactness in the regime tested.
- Decoded query-embedding probes show the embedding contains keyword content not present in the original query — the latent query is doing intermediate-reasoning expansion implicitly.

## Critique / open questions

- Evaluation is QA-only; unclear how the shared-space approach behaves on long-form generation, code, or settings where the retrieved passages are deeply structured rather than fact-bearing.
- The compressor depends on a strong teacher (Qwen-32B) for synthesis; circularity risk if the teacher's notion of "salient" mismatches the downstream task.
- 16× compression is reported as a sweet spot, but the failure mode at higher ratios (information collapse vs. graceful degradation) isn't characterized in the abstract.
- Embedding-compatibility question (NOTES.md open #1) is real: the compressor and the generator share base weights here, so drift is bounded — but this design assumes static retrieval; live encoding of in-flight text is unstudied.
- Latent queries are uninterpretable in the strict sense, but the keyword-decode trick (showing memory-token decodes contain reasoning hops) is a useful proxy this project should adopt.

## Trust signals

- **Credibility:** 4 — Apple + U. Edinburgh; arXiv preprint, not yet peer-reviewed; official code released (apple/ml-clara).

## Follow-up

**Relevance:** 5 — direct hit on design-move 1 (latent queries against a latent index) and design-move 3 (retrieval as a layer with gradient flow). Anchors the `latent-query`, `latent-index`, and `retrieval-as-layer` concepts. Implementation available at github.com/apple/ml-clara.

- Read code at github.com/apple/ml-clara before drafting the project's first experiment proposal.
- The keyword-decode probe (Fig 1b in the paper) is a concrete answer to the "latent queries are uninterpretable" open question — adopt as a debugging proxy.
- Consider whether SCP's QA+paraphrase synthesis target is the right pretraining signal for *code* corpora (the project's planned cross-file completion experiment) or whether it needs a domain-specific salient-info recipe.
