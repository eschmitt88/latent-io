---
kind: paper
title: "What Do Latent Action Models Actually Learn?"
authors: ["Chuheng Zhang", "Tim Pearce", "Pushi Zhang", "Kaixin Wang", "Xiaoyu Chen", "Wei Shen", "Li Zhao", "Jiang Bian"]
institutions: ["Microsoft Research", "Tsinghua University"]
year: 2025
venue: "arXiv (Microsoft Research, Tsinghua)"
peer_reviewed: false
url: "https://arxiv.org/abs/2506.15691"
code_url: null
citations: null
source: "raw/papers/zhang2025what.pdf"
added: "2026-05-04"
relevance: 4
credibility: 4
status: skimmed
related_experiments: []
related_concepts: ["action-observation-trace"]
tags: ["analysis", "latent-action", "pca", "controllable-vs-noise"]
---

# What Do Latent Action Models Actually Learn?

## TL;DR

Analytical study of LAMs as a linear model that captures the essence of LAM learning while remaining tractable. Shows connections between LAM and PCA, characterizes desiderata of the data-generating policy, and justifies strategies to encourage learning *controllable* changes (data augmentation, data cleaning, auxiliary action prediction) over irrelevant noise. Validated by simulations and more realistic experiments. First rigorous investigation of how observation/action/noise structure influences LAM learning.

## Claims

- LAM training can be analyzed as a linear-algebraic problem with structure analogous to PCA — provides clean intuition for what the latent dimension captures.
- The data-generating policy matters: certain policies bias the LAM toward learning agent-controllable change vs. exogenous noise.
- Three strategies provably help: data augmentation, data cleaning, and auxiliary action prediction.

## Methods

- Linear LAM model: tractable but captures essential dynamics.
- Analysis under various data-generating assumptions.
- Numerical and realistic-setting validation.

## Results

- Theoretical: PCA-like structure for what LAM captures.
- Empirical: data augmentation/cleaning/aux-prediction reliably improve latent quality.

## Critique / open questions

- Linear model is illuminating but obviously misses nonlinear LAM behavior in real architectures.
- "Controllable change" vs. "noise" is a useful dichotomy but real-world distinctions are messier.

## Trust signals

- **Credibility:** 4 — Microsoft Research + Tsinghua; arXiv preprint, not yet peer-reviewed; analytical study, no code link. Strong group offsets no code.

## Follow-up

**Relevance:** 4 — directly relevant to the "latent queries are uninterpretable" open question (NOTES.md #2). The PCA-like analysis is a probe template the project should adopt. Combined with LAOM's negative findings (`nikulin2025latent`), this paper is the analytical companion explaining *why* distractors confound LAM training and what to do about it.
