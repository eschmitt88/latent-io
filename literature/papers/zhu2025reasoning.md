---
kind: paper
title: "Reasoning by Superposition: A Theoretical Perspective on Chain of Continuous Thought"
authors: ["Hanlin Zhu", "Shibo Hao", "Zhiting Hu", "Jiantao Jiao", "Stuart Russell", "Yuandong Tian"]
year: 2025
venue: "arXiv (Berkeley, UCSD, Meta)"
url: "https://arxiv.org/abs/2505.12514"
source: "raw/papers/zhu2025reasoning.pdf"
added: "2026-05-04"
relevance: 4
status: skimmed
related_experiments: []
related_concepts: ["continuous-thought"]
tags: ["theory", "superposition", "expressivity", "graph-reachability"]
---

# Reasoning by Superposition: A Theoretical Perspective on Continuous Thought

## TL;DR

Theoretical analysis proving that a *two-layer* transformer with D steps of continuous CoT can solve directed-graph reachability where D is the diameter of the graph — far better than the best known result for constant-depth transformers with discrete tokens. Provides the formal grounding for why latent BFS outperforms greedy token CoT on planning tasks: continuous thoughts can hold a *superposition* of reasoning paths that discrete tokens cannot.

## Claims

- Continuous CoT is strictly more expressive than discrete CoT for reasoning problems with a search structure (graph reachability is the canonical example).
- The superposition interpretation of Coconut's continuous thoughts is formally valid: a continuous vector can encode multiple alternative reasoning paths simultaneously, then collapse to the right one when sufficient evidence accumulates.
- Two-layer transformers with continuous CoT solve graph reachability in O(D) steps; discrete-token analogs need depth or step counts that grow with problem size.

## Claims (continued — methods)

- Constructive proof: build a transformer that uses each continuous CoT step to maintain a superposition over reachable nodes, expanding with each iteration.
- Compares against best-known expressivity results for constant-depth transformers with discrete CoT.

## Results

- Theorem: 2-layer transformer + D continuous CoT steps solves directed-graph reachability for diameter D.
- This separates continuous-CoT from discrete-CoT in expressivity at constant depth.

## Critique / open questions

- Constructive proofs show what's *possible*; whether trained transformers actually use this superposition efficiently is empirical (Coconut's probes suggest yes, partially).
- Graph reachability is one specific problem class; the result should generalize to other search problems but isn't proven for all.

## Follow-up

**Relevance:** 4 — theoretical anchor for the load-bearing claim that latent has properties tokens don't. Critical citation when arguing the project's bet is more than an efficiency play. Pair with Coconut (`hao2024training`) — empirical demonstration + theoretical grounding.
