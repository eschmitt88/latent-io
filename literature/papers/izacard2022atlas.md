---
kind: paper
title: "Atlas: Few-shot Learning with Retrieval Augmented Language Models"
authors: ["Gautier Izacard", "Patrick Lewis", "Maria Lomeli", "Lucas Hosseini", "Fabio Petroni", "Timo Schick", "Jane Dwivedi-Yu", "Armand Joulin", "Sebastian Riedel", "Edouard Grave"]
year: 2022
venue: "JMLR 2023 (Meta AI)"
url: "https://arxiv.org/abs/2208.03299"
source: "raw/papers/izacard2022atlas.pdf"
added: "2026-05-04"
relevance: 3
status: skimmed
related_experiments: []
related_concepts: ["retrieval-as-layer", "latent-index"]
tags: ["foundational", "rag", "few-shot", "joint-training"]
---

# Atlas: Few-shot Learning with Retrieval Augmented Language Models

## TL;DR

A jointly pretrained encoder-decoder retrieval-augmented LM; treats retrieved documents as latent variables with the retriever and the generator updated together. With 11B parameters and an updateable index, Atlas reaches >42% on Natural Questions with only 64 examples — outperforming a 540B model by 3% with 50× fewer parameters.

## Claims

- Joint retriever-LM pretraining is necessary for *few-shot* knowledge tasks; pre-RAG few-shot baselines need massive parameter counts.
- Treating retrieved documents as latent variables (rather than text concatenations) lets the retriever learn from generation loss without explicit retrieval labels.
- The retrieval index is decoupled from model weights — updating the index updates the model's "knowledge" without retraining.

## Methods

- Encoder-decoder backbone (T5-style) trained with retrieval queries over an external index.
- Joint training: gradients propagate from generation loss back through the retriever via attention scores over candidates.
- Few-shot evaluation across MMLU, KILT, NaturalQuestions.

## Results

- 42% NaturalQuestions accuracy with 64 shots, 50× fewer params than a 540B baseline.
- Index swappability: replacing the index updates Atlas's knowledge without retraining.

## Critique / open questions

- Documents are treated as latent variables in *training objective*, not in representation — they're still text passed to a text encoder. The "latent" framing is statistical, not architectural.
- Retrieved documents are concatenated into the encoder context — long-context cost is real.

## Follow-up

**Relevance:** 3 — foundational prior, useful as the philosophical ancestor of "documents as latent variables" but architecturally less load-bearing for this project than CLaRa or LAnR.
