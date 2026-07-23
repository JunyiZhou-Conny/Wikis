---
title: "Gemma Scope: Open Sparse Autoencoders Everywhere All At Once on Gemma 2"
type: source
status: done
date: 2026-07-23
source_kind: paper
tier: A
venue: "BlackboxNLP (ACL workshop)"
year: 2024
authors: ["Lieberum", "Rajamanoharan", "Conmy", "Smith", "Sonnerat", "Varma", "Kramár", "Dragan", "Shah", "Nanda"]
approx_citations: 160
doi: "10.18653/v1/2024.blackboxnlp-1.19"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/autoencoder
  - method/sparse-autoencoder
  - method/autoencoder
---

# Gemma Scope: Open Sparse Autoencoders Everywhere All At Once on Gemma 2

Lieberum, Rajamanoharan, Conmy, Smith, Sonnerat, Varma, Kramár, Dragan, Shah, Nanda
(Google DeepMind), *BlackboxNLP* 2024. Open release of **JumpReLU SAEs on every layer
and sublayer** of Gemma 2 — the first comprehensive public SAE suite for a modern open LM.

## Summary

Training a full SAE suite is expensive enough that most community work stays on small models
or single residual-stream sites. Gemma Scope removes that bottleneck by releasing **>400
JumpReLU SAEs** (thousands counting sparsity sweeps) covering attention-prelinear, MLP-output,
and post-MLP residual sites on Gemma 2 2B/9B (plus selected 27B layers and IT residuals).
Weights are CC-BY-4.0 on Hugging Face; evaluations report sparsity–fidelity curves (delta LM
loss, FVU) so downstream researchers can pick SAEs without retraining.

## Key claims / results

- **Comprehensive open coverage:** JumpReLU SAEs on *all* layers and three sites for Gemma 2
  2B and 9B PT, select residual layers for 27B, plus IT residual SAEs and one transcoder suite —
  enabling multi-site circuit work that single-layer releases cannot support.
- **Scale of release:** >30M learned latents in the main release; training used a substantial
  fraction of GPT-3-scale compute and ~20 PiB of stored activations; widths from ~16K to ~1M.
- **Sparsity–fidelity trade-offs are site-dependent:** residual-stream SAEs incur higher *delta
  LM loss* than MLP/attention SAEs at similar FVU, because residual error hits the whole
  forward pass.
- **Width ladder for feature splitting:** matched-sparsity residual SAEs from 16.4K–524K width
  at mid-network layers let researchers study how wider dictionaries split vs broaden features.
- **Position effects:** reconstruction loss rises over the first tokens then plateaus; attention
  SAEs keep rising longer than MLP SAEs, consistent with long-range vs local processing.

## Methodology

- **Architecture:** JumpReLU SAEs — per-latent learned threshold gates a ReLU; train with MSE
  reconstruction + L0 sparsity, using straight-through estimators for the discontinuous
  threshold (bandwidth ε = 0.001 after unit-mean-squared-norm input normalization).
- **Sites per block:** attention-head outputs *before* the final linear + RMSNorm; MLP outputs
  *after* RMSNorm; post-MLP residual stream (Fig. 1 in the paper).
- **Training:** Adam; decoder columns unit-normalized each step; pre-encoder bias folded into
  encoder at export; 4–16B tokens depending on width; multiple L0 targets released per site.
- **Eval:** mean L0; delta cross-entropy when the SAE is spliced into the LM; FVU / normalized
  reconstruction loss; sweeps over sparsity, width, sequence position, and PT vs IT.

## Related

- extends [[2023-bricken-towards-monosemanticity]] — same SAE-for-monosemanticity agenda, scaled from a 512-neuron toy MLP to full open Gemma 2 layer/sublayer coverage
- extends [[2006-hinton-deep-autoencoder]] — reconstructive AE skeleton retained, but deployed as an overcomplete JumpReLU dictionary on frozen LM activations rather than a compressive bottleneck
- applies [[sparse-autoencoder-dictionary-learning]] — JumpReLU + L0 as the dictionary-learning objective at production-LM scale
- applies [[monosemantic-features-vs-polysemantic-neurons]] — open weights so the community can test whether Gemma latents behave as monosemantic features
- introduces [[open-layerwise-sae-suite]] — releasing matched SAEs at every layer/site as infrastructure, not a single-site demo
- [[Sources MOC]]
- [[Autoencoder MOC]]
