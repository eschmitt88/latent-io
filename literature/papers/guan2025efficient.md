---
kind: paper
title: "Efficient Vision-Language-Action Models for Embodied Manipulation: A Systematic Survey"
authors: ["Weifan Guan", "Qinghao Hu", "Aosheng Li", "Jian Cheng"]
year: 2025
venue: "arXiv (CAS, AiRiA)"
url: "https://arxiv.org/abs/2510.17111"
source: "raw/papers/guan2025efficient.pdf"
added: "2026-05-04"
relevance: 2
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

## Follow-up

**Relevance:** 2 — orientation. Useful for understanding architectural patterns at the latent-action / token boundary. Read once when seeding the action-observation-trace concept; not load-bearing.
