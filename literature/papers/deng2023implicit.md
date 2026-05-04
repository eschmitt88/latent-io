---
kind: paper
title: "Implicit Chain of Thought Reasoning via Knowledge Distillation"
authors: ["Yuntian Deng", "Kiran Prasad", "Roland Fernandez", "Paul Smolensky", "Vishrav Chaudhary", "Stuart Shieber"]
year: 2023
venue: "arXiv (Harvard, AI2, Microsoft, JHU)"
url: "https://arxiv.org/abs/2311.01460"
source: "raw/papers/deng2023implicit.pdf"
added: "2026-05-04"
relevance: 3
status: skimmed
related_experiments: []
related_concepts: ["continuous-thought"]
tags: ["foundational", "implicit-cot", "knowledge-distillation", "vertical-reasoning"]
---

# Implicit Chain of Thought Reasoning via Knowledge Distillation

## TL;DR

Distill explicit-CoT teacher *hidden states* into a student model, so the student reasons "vertically" through layers without producing intermediate text — instead of "horizontally" by emitting words one at a time. The student does its multi-step reasoning across the depth dimension instead of the time dimension.

## Claims

- People reason in natural language because the language exists; nothing about the underlying computation requires it. LMs may reason more effectively with intermediate representations that aren't natural language.
- Cross-layer (vertical) reasoning is a real alternative to cross-token (horizontal) reasoning; the layers in a deep transformer can carry the multi-step structure that CoT lays out across tokens.
- Distillation from an explicit-CoT teacher's hidden states transfers the reasoning structure into the student's layer-internal computation.

## Methods

- "Thought emulation": the student LM is trained to imitate the teacher's hidden-state trajectory rather than its surface tokens.
- Evaluated on multi-step reasoning tasks (math word problems and similar).

## Results

- Student matches or approaches teacher's reasoning accuracy without producing text intermediates.

## Critique / open questions

- Strong dependence on a quality teacher; circularity risk with imperfect supervision.
- The distillation signal that makes this work — gradient flow from a richly-CoT-supervised teacher's hidden states — is exactly what CODI (`shen2025codi`) later replaces with self-distillation.

## Follow-up

**Relevance:** 3 — historical baseline. The "reason vertically through layers, not horizontally through tokens" framing is foundational for both `retrieval-as-layer` (which also lives across layers) and `continuous-thought`. Useful early citation.
