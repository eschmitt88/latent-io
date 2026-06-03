---
kind: paper
title: "Memory in Large Language Models: Mechanisms, Evaluation and Evolution"
authors: ["Dianxing Zhang", "Wendong Li", "Kani Song", "Jiaye Lu", "Gang Li", "Liuchun Yang", "Sheng Li"]
institutions: ["Digital China AI Research Institute"]
year: 2025
venue: "arXiv (Digital China AI Research)"
peer_reviewed: false
url: "https://arxiv.org/abs/2509.18868"
code_url: null
citations: null
source: "raw/papers/zhang2025memory.pdf"
added: "2026-05-04"
relevance: 2
credibility: 2
status: skimmed
related_experiments: []
related_concepts: ["latent-index"]
tags: ["survey", "memory", "evaluation", "taxonomy"]
---

# Memory in LLMs: Mechanisms, Evaluation and Evolution

## TL;DR

Operational definition of LLM memory as "a persistent state that is written during pretraining, finetuning, or inference, can be subsequently addressed, and stably influences outputs," organized into a four-way taxonomy (parametric, contextual, external, procedural/episodic) and evaluated under a three-setting protocol (parameter-only, offline retrieval, online retrieval) that decouples model capability from information availability.

## Claims

- A unified definition + memory-quadruple (storage, persistence, write/access path, controllability) lets cross-paper comparison work where it currently doesn't.
- Decoupling capability from information availability via parallel evaluation settings is the right way to measure memory contributions.
- Layered evaluation: closed-book recall + edit differential for parametric, position-performance curves for contextual, snippet-level attribution for external, cross-session consistency for procedural.

## Methods (as a survey)

- Taxonomy + evaluation protocol synthesis.
- Discusses temporal governance, write/read/inhibit/update causal chains.

## Results

N/A — survey.

## Critique / open questions

- A taxonomy is only as useful as the projects that adopt it. The four-way split is reasonable but architecturally coarse — "external memory" lumps RAG with persistent KV caches with vector stores.

## Trust signals

- **Credibility:** 2 — Digital China AI Research; arXiv survey, no peer review; no code. Industrial single-org survey, mixed signals.

## Follow-up

**Relevance:** 2 — orientation. Useful for catching prior art on procedural/episodic memory the project's framing doesn't naturally surface. Skim once when seeding `concepts/`; not a load-bearing primary read.
