---
kind: paper
title: "Efficient Vision-Language-Action Models for Embodied Manipulation: A Systematic Survey"
authors: ["Weifan Guan", "Qinghao Hu", "Aosheng Li", "Jian Cheng"]
institutions: ["Institute of Automation, Chinese Academy of Sciences", "University of Chinese Academy of Sciences", "AiRiA", "Nanjing University of Information Science and Technology"]
year: 2025
venue: "arXiv (CAS, AiRiA)"
peer_reviewed: false
url: "https://arxiv.org/abs/2510.17111"
code_url: "https://github.com/Awesome-Efficient-VLA"
citations: null
source: "raw/papers/guan2025efficient.pdf"
added: "2026-05-04"
relevance: 2
credibility: 3
status: skimmed
related_experiments: []
related_concepts: []
tags: ["survey", "vla", "embodied", "efficiency"]
---

# Efficient Vision-Language-Action Models: A Systematic Survey

## TL;DR

Systematic review of approaches for improving VLA efficiency across four dimensions: model architecture, perception feature, action generation, and training/inference strategies. Covers latency, memory footprint, and training/inference cost reductions, with emphasis on edge-platform deployment.

## Claims (as a survey)

- VLA efficiency is the bottleneck for embodied deployment; massive computational and memory demands conflict with edge platform constraints.
- Four-dimensional taxonomy organizes the field: architecture, features, action generation, training/inference.
- Latent-action interfaces appear under "action generation" as one of the major architectural patterns for efficient VLA.

## Trust signals

- **Credibility:** 3 — CAS/UCAS/AiRiA survey; arXiv preprint, no peer review; companion GitHub paper list. Reputable group, survey scope.

## Follow-up

**Relevance:** 2 — orientation. Useful for understanding architectural patterns at the latent-action / token boundary. Read once when seeding the action-observation-trace concept; not load-bearing.
