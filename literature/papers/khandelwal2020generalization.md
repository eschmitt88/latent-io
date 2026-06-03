---
kind: paper
title: "Generalization through Memorization: Nearest Neighbor Language Models (kNN-LM)"
authors: ["Urvashi Khandelwal", "Omer Levy", "Dan Jurafsky", "Luke Zettlemoyer", "Mike Lewis"]
institutions: ["Stanford University", "Facebook AI Research"]
year: 2020
venue: "ICLR 2020"
peer_reviewed: true
url: "https://arxiv.org/abs/1911.00172"
code_url: null
citations: null
source: "raw/papers/khandelwal2020generalization.pdf"
added: "2026-05-04"
relevance: 4
credibility: 5
status: skimmed
related_experiments: []
related_concepts: ["latent-index", "retrieval-as-layer"]
tags: ["foundational", "knn", "interpolation", "datastore"]
---

# kNN-LM: Generalization through Memorization

## TL;DR

Augment a pretrained LM by linearly interpolating its next-token distribution with a kNN distribution computed over neighbours retrieved from a datastore — neighbours are computed in the LM's own embedding space, requires no retraining, and yields SOTA Wikitext-103 perplexity (15.79) with effective domain adaptation by swapping the datastore.

## Claims

- Learning *similarity* between sequences is easier than learning *next-word prediction* — kNN over LM hidden states can leverage that.
- The same model can be made to generalize better by adding non-parametric memory; no extra training needed.
- Domain adaptation reduces to switching out the datastore.

## Methods

- For each context in the training set, store `(LM hidden state, next token)` pairs in a datastore.
- At inference, retrieve k nearest contexts by L2 distance in hidden-state space; convert distances to a softmax distribution over their target tokens.
- Interpolate the LM's softmax with the kNN softmax via a fixed coefficient λ.

## Results

- Wikitext-103 perplexity: 15.79 (SOTA at the time, 2.9-pt improvement over the base LM, no extra training).
- Particularly strong on rare/factual patterns — i.e. the long tail.
- Effective domain adaptation by datastore swap.

## Critique / open questions

- Datastore is enormous (one entry per training context) and expensive to query at inference.
- λ is fixed — no learned uncertainty-driven gating, which later work (LAnR) addresses.
- Retrieval is *additive* over the LM's logits, not integrated into the residual stream — closer to "ensemble of LM and kNN" than "retrieval as a layer".

## Trust signals

- **Credibility:** 5 — Stanford + FAIR; ICLR 2020 peer-reviewed; foundational kNN-LM, heavily cited. No code link in note but widely reproduced.

## Follow-up

**Relevance:** 4 — the foundational ancestor of "retrieve in LM embedding space". Architecturally the simplest possible latent retrieval, which makes it a useful baseline and a sanity check on whether more elaborate latent-retrieval architectures are buying real capability vs. just efficiency.
