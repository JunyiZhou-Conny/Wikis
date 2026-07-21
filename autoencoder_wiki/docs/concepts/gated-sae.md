---
title: Gated sparse autoencoder
type: concept
status: done
date: 2026-07-21
tags:
  - concept
  - domain/ml
  - topic/autoencoder
  - method/sparse-autoencoder
distilled_from:
  - "[[2024-rajamanoharan-gated-saes]]"
  - "[[2023-bricken-towards-monosemanticity]]"
---

# Gated sparse autoencoder

A **Gated SAE** splits the encoder into a **gate** (which features are active) and a
**magnitude** path (how strongly they fire). The L1 sparsity penalty hits only the gate, so
it no longer systematically **shrinks** live feature activations.

## Why it matters / where it shows up

Standard L1-ReLU SAEs ([[2023-bricken-towards-monosemanticity]]) under-estimate active feature
magnitudes because L1 penalizes size as well as count. Gated SAEs
([[2024-rajamanoharan-gated-saes]]) confine that penalty to feature *selection*, yielding a
better sparsity–fidelity Pareto frontier on LM activations (up to Gemma-7B) while keeping
parameter count close via weight tying. The tied form is mathematically a **JumpReLU**-style
thresholded linear encoder — the architectural seed for later JumpReLU SAE training.

## Details

- **Encoder:** \(\tilde{f}=\mathbf{1}[\pi_{\mathrm{gate}}>0]\odot\mathrm{ReLU}(\pi_{\mathrm{mag}})\);
  \(W_{\mathrm{mag}}\) shares directions with \(W_{\mathrm{gate}}\), differing by a positive
  per-feature scale and separate biases.
- **Loss:** MSE on the gated reconstruction + \(\lambda\|\mathrm{ReLU}(\pi_{\mathrm{gate}})\|_1\)
  + auxiliary MSE from gate pre-activations through a frozen decoder copy.
- **Shrinkage diagnostic:** relative reconstruction bias \(\gamma\approx 1\) (unbiased) vs
  \(\gamma<1\) for baseline L1-ReLU.
- **Cost:** ~1.5× compute per training step (decoder run twice); inference stays cheap with tying.

## Related

- introduces [[2024-rajamanoharan-gated-saes]] — architecture, gated loss, Gemma/Pythia Pareto and shrinkage evals
- contrasts [[2023-bricken-towards-monosemanticity]] — L1 on full ReLU activations (shrinkage) vs L1 on gate only
- applies [[sparse-autoencoder-dictionary-learning]] — same overcomplete dictionary goal, gated activation
- background-for [[monosemantic-features-vs-polysemantic-neurons]] — fidelity/sparsity gains claimed without hurting blinded interpretability ratings
