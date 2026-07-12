---
title: "Extracting and Composing Robust Features with Denoising Autoencoders"
type: source
status: done
date: 2026-07-12
source_kind: paper
tier: A
venue: "ICML"
year: 2008
authors: ["Vincent", "Larochelle", "Bengio", "Manzagol"]
approx_citations: 10000
doi: "10.1145/1390156.1390294"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/autoencoder
  - method/denoising-autoencoder
  - method/autoencoder
---

# Extracting and Composing Robust Features with Denoising Autoencoders

Vincent, Larochelle, Bengio & Manzagol, *ICML* 2008. The **canonical denoising autoencoder
(DAE)** paper — trains an AE to reconstruct a clean input from a deliberately corrupted one,
then stacks those layers to initialize deep nets.

## Summary

Deep nets were hard to train from random init; unsupervised layer-wise pretraining (RBMs,
stacked AEs) helped, but it was unclear what makes a "good" intermediate representation. The
authors propose an extra criterion: **robustness to partial destruction of the input**. A
**denoising autoencoder** corrupts each training example (here: randomly zero a fraction ν of
coordinates), encodes the corrupted vector, and reconstructs the *original* clean input. Stacked
DAEs (SdA) initialize deep classifiers that beat stacked clean autoencoders on most of a hard
MNIST-variation benchmark, and often match or beat DBNs.

## Key claims / results

- **Corruption + reconstruction** yields more useful features than clean autoencoding: on the
  Larochelle et al. (2007) suite, SdA-3 matches or beats SAA-3 (ν=0) on almost every task and is
  best or tied-best vs SVMs / DBN-1 / DBN-3 except `bg-rand`.
- Denoising **removes the identity-map trap**, so overcomplete hidden layers (e.g. 2000 units on
  784-d MNIST) become usable without an explicit bottleneck or weight-decay crutch.
- Filter visualizations: with ν=0 many first-layer filters stay uninteresting; raising destruction
  (25%→50%) produces sharper detectors and **less local** filters sensitive to larger structure.
- The training objective can be read as **manifold projection** (map corrupted off-manifold
  points back), as maximizing a **variational bound** on a particular generative model, and as
  maximizing a lower bound on **mutual information** I(X;Y) when Y is a function of corrupted X.

## Methodology

- **Basic AE:** y = s(Wx + b), z = s(W'y + b'); minimize reconstruction loss (squared error or
  Bernoulli cross-entropy L_IH) on clean x.
- **DAE:** sample x̃ ∼ q_D(x̃|x) by zeroing νd random coordinates; encode y = f_θ(x̃); decode z;
  minimize E[L_IH(x, z)] so z matches the *uncorrupted* x.
- **Stacking:** train layer k with the DAE criterion on (uncorrupted) outputs of layers below;
  corruption is training-only. Then supervised fine-tune the full deep net.
- **Eval:** 3-hidden-layer nets (SdA-3) on MNIST variants (basic, rot, bg-rand, bg-img,
  rot-bg-img) plus rect / rect-img / convex; model-select ν, widths, unsupervised epochs with
  early-stopped fine-tuning.

## Related

- extends [[2006-hinton-deep-autoencoder]] — same deep AE / layer-wise pretraining lineage, but
  replaces clean reconstruction with an explicit corruption+denoising criterion
- background-for [[2019-eraslan-dca]] — classic "reconstruct clean from corrupted" idea; DCA
  specializes denoising to scRNA count noise models rather than generic input blanking
- contrasts [[2023-bricken-towards-monosemanticity]] — input-space corruption for robust stacked
  features vs overcomplete L1-sparse SAE dictionary learning for monosemantic LM features
- introduces [[denoising-autoencoder-corruption-robustness]] — DAE as robustness-to-corruption
  representation learning
- contrasts [[sparse-autoencoder-dictionary-learning]] — both unlock overcomplete codes, via
  denoising vs sparsity penalties
- [[Sources MOC]]
- [[Autoencoder MOC]]
