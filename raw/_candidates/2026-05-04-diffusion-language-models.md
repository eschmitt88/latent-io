---
kind: candidates
topic: "diffusion language models"
discovered: 2026-05-04
source: discover
n_requested: 10
n_returned: 10
---

# Diffusion language models — triage 2026-05-04

Ranked by relevance to the membrane framing. Diffusion LMs matter to
this project not as a competing paradigm but because they sidestep the
strict autoregressive commitment — useful evidence on what a *non-AR*
generation interface looks like, and where the natural commitment
boundary lives. Direct hits and foundational priors first; coding-domain
work next (matches the planned cross-file completion experiment); surveys
at the bottom.

## 1. LLaDA: Large Language Diffusion Models

- url: https://arxiv.org/abs/2502.09992
- type: paper
- summary: ML-GSAI's 8B masked diffusion model trained from scratch on standard LM data; rivals LLaMA3 8B on in-context learning and instruction following, demonstrating that AR is not a prerequisite for LM capabilities at scale.
- reason: The strongest existence proof that a non-AR generation interface scales — relevant to the project's question of how strict token-level commitment is. Code at github.com/ML-GSAI/LLaDA is a viable base model for a latent-IO experiment that wants flexible generation order.

## 2. Score Entropy Discrete Diffusion (SEDD)

- url: https://arxiv.org/abs/2310.16834
- type: paper
- summary: Lou, Meng, Ermon (ICML 2024 Best Paper) introduce score entropy as the discrete analogue of the score function and use it to train a discrete diffusion LM that achieves 6–8× better generative perplexity than GPT-2 with 32× fewer network evaluations.
- reason: Theoretical foundation for the modern wave of diffusion LMs. Required reading to understand what the loss function is actually doing in latent space, which matters when designing the project's latent training objective.

## 3. Simple and Effective Masked Diffusion Language Models (MDLM)

- url: https://s-sahoo.com/mdlm/
- type: paper
- summary: Kuleshov-group / Sahoo et al. (NeurIPS 2024) show that a Rao-Blackwellized masked-diffusion objective is sharper and more performant than prior recipes; provides the cleanest training pipeline for masked-diffusion LMs.
- reason: The "minimum viable" diffusion LM recipe — a sane starting point if a project experiment needs a small, trainable diffusion baseline. Code at github.com/kuleshov-group/mdlm.

## 4. DiffuCoder: Understanding and Improving Masked Diffusion Models for Code Generation

- url: https://arxiv.org/abs/2506.20639
- type: paper
- summary: Apple's 7B masked-diffusion model trained on 130B code tokens. Defines an "AR-ness" metric showing dLLMs become *less* left-to-right when generating code, and introduces coupled-GRPO RL for non-AR objectives.
- reason: Directly relevant to the cross-file code-completion experiment proposed in NOTES.md — code is the strongest demonstrated case where strict AR commitment is suboptimal. The AR-ness metric is exactly the kind of measurement the project will need to argue tokens are bottlenecking latent cognition.

## 5. Mercury: Ultra-Fast Language Models Based on Diffusion

- url: https://arxiv.org/abs/2506.17298
- type: paper
- summary: Inception Labs' Mercury family — the first commercial-scale diffusion LLMs, with Mercury Coder Mini matching GPT-4o-Mini quality at ~4× the speed and Mercury 2 reaching 1000+ tokens/s. Demonstrates production deployability of non-AR generation.
- reason: Relevant evidence that a non-token-by-token commitment regime is not just a research curiosity — it ships. Useful as motivation in proposals: the inefficiency of strict AR commitment is real enough to displace it commercially.

## 6. Dream-Coder 7B: An Open Diffusion Language Model for Code

- url: https://arxiv.org/abs/2509.01142
- type: paper
- summary: Open 7B discrete diffusion LM for code that adaptively chooses sketch-first, left-to-right, or interleaved-reasoning decoding based on the coding task; competitive with leading code LLMs.
- reason: Open alternative to Apple's DiffuCoder for the planned code-completion experiment. The adaptive decoding strategy (sketch vs. left-to-right) is concretely the kind of "commitment policy" the project needs to study at the membrane.

## 7. ReFusion: A Diffusion LLM with Parallel Autoregressive Decoding

- url: https://arxiv.org/html/2603.22075v1
- type: paper
- summary: ML-GSAI (ICLR 2026) hybridize masked-diffusion with parallel AR decoding, yielding 34% perf gain over prior MDMs and 18× speed up versus AR baselines.
- reason: Most recent attempt to land between AR and pure diffusion — directly explores where the right "commitment granularity" sits, which is the same question the project is asking about token vs. latent boundaries. Code at github.com/ML-GSAI/ReFusion.

## 8. A Survey on Diffusion Language Models (VILA-Lab)

- url: https://github.com/VILA-Lab/Awesome-DLMs
- type: repo
- summary: Curated repo backing the official "Survey on Diffusion Language Models" — comprehensive paper list, taxonomy of approaches, training recipes, and evaluation benchmarks.
- reason: Cheap orientation read for surveying the field before drafting `concepts/` notes on commitment-boundary and latent generation. Use as a standing index, not for primary insight.

## 9. Discrete Diffusion in Large Language and Multimodal Models: A Survey

- url: https://arxiv.org/abs/2506.13759
- type: paper
- summary: Comprehensive survey covering discrete-diffusion theory, continuous-time formulations, masked vs. score-based variants, and multimodal extensions across text/image/code.
- reason: Better than the awesome-list as a single read. Particularly useful for the multimodal angle, since the project's broader framing (film-as-N-channel-signal, scale-conditional latent) connects to multimodal diffusion.

## 10. Autoregressive vs. Masked Diffusion Language Models: A Controlled Comparison

- url: https://arxiv.org/html/2603.22075v1
- type: paper
- summary: Controlled comparison evaluating MDM vs. AR LMs at matched compute, isolating where each paradigm wins or loses; provides cleaner head-to-head numbers than scattered single-model claims.
- reason: Useful methodological reference. Any project experiment that argues "latent/non-AR helps" needs a rigorous controlled comparison rather than an apples-to-oranges scaling claim — this paper is a template for that.
