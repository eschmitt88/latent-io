---
kind: paper
title: "Generation-Augmented Generation: A Plug-and-Play Framework for Private Knowledge Injection in LLMs"
authors: ["Rongji Li", "Jian Xu", "Yi Chen", "Xueqing Chen", "Yisheng Yang", "Jiayi Wang", "Xingyu Chen", "Chunyu Xie", "Dawei Leng", "Xu-Yao Zhang"]
institutions: ["Institute of Automation, Chinese Academy of Sciences / UCAS / Zhongguancun Academy", "360 AI Research"]
year: 2026
venue: "ACM MM 2026 (CAS / 360 AI Research)"
peer_reviewed: true
url: "https://arxiv.org/abs/2601.08209"
code_url: null
citations: null
source: "raw/papers/li2026generation.pdf"
added: "2026-05-04"
relevance: 4
credibility: 3
status: skimmed
related_experiments: []
related_concepts: ["retrieval-as-layer", "latent-index"]
tags: ["latent-injection", "frozen-base", "domain-adaptation", "gated-residual"]
---

# Generation-Augmented Generation (GAG): Plug-and-Play Latent Knowledge Injection

## TL;DR

A retrieval-free knowledge-injection framework that distills question-conditioned domain knowledge from lightweight expert models into multi-slot latent memories and injects them into a frozen base LLM via per-slot cross-layer fusion and gated residual projection — no base parameter updates, constant-budget latent interface, prototype-based plug-and-play routing for multiple domains.

## Claims

- Private-domain knowledge injection has two unsatisfying defaults: fine-tuning (catastrophic forgetting, expensive iteration) and RAG (long contexts, high inference cost). A latent injection that touches neither is preferable.
- A constant-budget set of latent memory slots, fused across layers and gated into the residual stream, can carry domain knowledge without modifying the base model.
- Prototype routing over memory slots enables multi-domain deployment without per-domain fine-tuning.

## Methods

- Lightweight expert models are trained per private domain and emit question-conditioned knowledge as multi-slot latent memories.
- Memories are fused across layers and injected into the frozen base via gated residual projection — the gate decides per-slot whether and how strongly to inject.
- Routing: prototype-based selector activates the right domain expert(s) at inference.
- Evaluated on catalytic-materials and immunology-adjuvant private-domain QA + general-domain queries.

## Results

- Outperforms strong retrieval and PEFT baselines on specialist QA while preserving general-domain performance.
- Reliable routing across mixed-domain workloads.
- Reduced token-overhead and long-context burden vs. RAG.

## Critique / open questions

- "Plug-and-play" depends on the experts staying compatible with the base's residual-stream geometry — drift in either side breaks the gate.
- Multi-slot memory is constant-budget per expert but scales linearly in number of experts.
- Evaluation is QA-focused; whether the latent interface carries enough bandwidth for *generation*-heavy domain tasks (long-form synthesis, code) is untested.

## Trust signals

- **Credibility:** 3 — CAS + 360 AI Research; ACM MM 2026 peer-reviewed; no code link in note. Venue lifts it; reproducibility unverified.

## Follow-up

**Relevance:** 4 — strong concrete instance of design-move 3. Gated residual projection is exactly the mechanism this project needs to think through for *retrieval* injection (the same gate idea applies whether the slots come from a retriever or an expert head).

- Worth comparing the GAG slot-injection mechanism with CLaRa's memory-token approach when designing the project's own latent interface.
- Code at github.com/360CVGroup/GAG.
