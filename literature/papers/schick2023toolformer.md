---
kind: paper
title: "Toolformer: Language Models Can Teach Themselves to Use Tools"
authors: ["Timo Schick", "Jane Dwivedi-Yu", "Roberto Dessì", "Roberta Raileanu", "Maria Lomeli", "Luke Zettlemoyer", "Nicola Cancedda", "Thomas Scialom"]
institutions: ["Meta AI Research", "Universitat Pompeu Fabra"]
year: 2023
venue: "NeurIPS 2023 (Meta AI)"
peer_reviewed: true
url: "https://arxiv.org/abs/2302.04761"
code_url: null
citations: null
source: "raw/papers/schick2023toolformer.pdf"
added: "2026-05-04"
relevance: 3
credibility: 5
status: skimmed
related_experiments: []
related_concepts: ["commitment-boundary"]
tags: ["foundational", "tool-use", "self-supervised", "api-calls", "token-emitted"]
---

# Toolformer: Self-Supervised Tool Use

## TL;DR

LMs teach themselves to use external tools via simple APIs by inserting candidate API calls into pretraining text and keeping only those calls that *reduce perplexity* on the surrounding tokens. Trains the model to autonomously decide when to call tools and how to use the results, using nothing more than a handful of demonstrations per API. Substantially improves zero-shot performance with no degradation to core LM ability.

## Claims

- Tool use can be learned without human-annotated tool-call traces. The perplexity-reduction signal — does this API call make the next tokens easier to predict? — is sufficient supervision.
- Tools should be *self-supervised*: the model decides which calls help and learns from those.
- Adding tool-use to an LM doesn't sacrifice core LM ability when done this way.

## Methods

- For each API and each pretraining text passage, sample candidate API call positions and arguments using few-shot demonstrations.
- Execute each candidate call; keep only those whose result, inserted into the text, reduces the LM's perplexity on subsequent tokens.
- Fine-tune the LM on the kept examples.

## Results

- Substantial zero-shot gains on tasks where tools help (math, factual QA, translation, calendar).
- No degradation on standard LM benchmarks.
- A 6.7B-parameter Toolformer is competitive with much larger models on tool-using tasks.

## Critique / open questions

- Calls are token-emitted; the model commits to a tool, arguments, and decoded result through the token interface — exactly the regime this project is arguing against.
- No chaining: each call is generated independently; the output of one call cannot be the input to another within the same generation.

## Trust signals

- **Credibility:** 5 — Meta AI; NeurIPS 2023 peer-reviewed; widely cited foundational tool-use work. No code link in note.

## Follow-up

**Relevance:** 3 — the canonical reference point for the *token-emitted* tool-use regime. Reading it carefully clarifies what's hard about pulling tool-use into latent: the perplexity-reduction signal that makes Toolformer's self-supervision work is what any latent-tool variant will need to find an analogue of.
