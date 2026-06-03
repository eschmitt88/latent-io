---
kind: paper
title: "MLP Memory: A Retriever-Pretrained Memory for Large Language Models"
authors: ["Rubin Wei", "Jiaqi Cao", "Jiarui Wang", "Jushi Kai", "Qipeng Guo", "Bowen Zhou", "Zhouhan Lin"]
institutions: ["LUMIA Lab, Shanghai Jiao Tong University", "Shanghai AI Laboratory", "Tsinghua University"]
year: 2025
venue: "arXiv (LUMIA Lab, SJTU)"
peer_reviewed: false
url: "https://arxiv.org/abs/2508.01832"
code_url: "https://github.com/LUMIA-Group/MLPMemory"
citations: null
source: "raw/papers/wei2025mlp.pdf"
added: "2026-05-04"
relevance: 3
credibility: 4
status: skimmed
related_experiments: []
related_concepts: ["latent-index"]
tags: ["parametric-memory", "retriever-distillation", "knn-substitute", "alternative-architecture"]
---

# MLP Memory: A Retriever-Pretrained Memory

## TL;DR

Replaces kNN-LM's vector datastore with a fully parameterized MLP that is pretrained to imitate the kNN retriever's output distribution over the entire pretraining corpus. The pretrained MLP is integrated with a Transformer decoder via simple probability interpolation, yielding 17.5–24.1% scaling gains, 12.3% relative QA improvement, and 2.5× faster inference than RAG with no nearest-neighbour search at inference time.

## Claims

- Retrieval *patterns* — what kNN over a pretraining corpus would return — can be baked into a small parametric module without storing the corpus.
- Doing so eliminates the inference latency and storage cost of non-parametric retrieval (220 GB → 2.8 GB; 80× faster lookup) while keeping most of the benefit.
- The resulting memory is differentiable end-to-end, so it composes with downstream training cleanly.

## Methods

- Pretrain an MLP to predict the kNN-LM's next-token distribution over the entire pretraining corpus (i.e. distill the retriever's behaviour into MLP weights).
- Integrate via probability interpolation with the base LM, identical interface to kNN-LM.

## Results

- Wikitext-103 / Web scaling gains: 17.5% / 24.1%.
- 12.3% relative QA improvement across 5 benchmarks.
- 5.2 absolute point gain on 9 general NLP tasks.
- Up to 10-point HaluEval reduction in hallucinations.
- 2.5× faster than RAG at higher accuracy.

## Critique / open questions

- The MLP is now a static snapshot of the corpus — updating knowledge requires re-distilling, which negates kNN-LM's "swap the datastore" advantage.
- Distilling from a kNN target locks the system to whatever the kNN retriever was good at; if the retriever was suboptimal, the MLP inherits the suboptimality without the index's flexibility to be repaired.

## Trust signals

- **Credibility:** 4 — SJTU LUMIA + Shanghai AI Lab + Tsinghua; arXiv preprint, not yet peer-reviewed; code + HF collection released (LUMIA-Group/MLPMemory).

## Follow-up

**Relevance:** 3 — interesting alternative answer to "where does the latent index live": don't use a vector store, parameterize the retriever's output distribution directly. Useful contrast for the project's bet on external latent indices, and a live alternative to keep in mind for the embedding-compatibility open question.
