---
title: "k-Sparse Autoencoders"
type: source
status: done
date: 2026-07-18
source_kind: paper
tier: A
venue: "ICLR"
year: 2014
authors: ["Makhzani", "Frey"]
approx_citations: 570
doi: "10.48550/arXiv.1312.5663"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/autoencoder
  - method/sparse-autoencoder
  - method/autoencoder
---

# k-Sparse Autoencoders

Makhzani & Frey, *ICLR* 2014. Canonical **k-sparse autoencoder**: a linear AE whose only
nonlinearity / regularizer is keeping the **k largest** hidden activations (hard Top-k). The
classic root of the TopK SAE recipe used in modern mechanistic interpretability.

## Summary

Sparse feature learning often mixes activation choices, sampling tricks, and penalty terms, so it
is unclear what sparsity alone buys. This paper isolates sparsity by training a **tied-weight
linear autoencoder** that, after computing \(z = W^\top x + b\), **zeros all but the k largest
entries** and reconstructs from that support. Encoding is a matrix multiply plus a sort /
threshold — fast enough for large problems where classical sparse coding (OMP, K-SVD, …) is too
slow. On MNIST and NORB, unsupervised k-sparse features beat RBMs, dropout AEs, and denoising
AEs for linear classification, and the same block serves as a greedy layer-wise pretrainer.

## Key claims / results

- **Sparsity alone is enough:** with linear units and no L1 / KL / dropout / denoising, hard
  Top-k yields better unsupervised features than RBM, dropout AE, and denoising AE baselines
  (best MNIST: 1.35% with \(k=25\); best NORB: 8.6% with \(k=150\)).
- **Exact per-example sparsity:** unlike lifetime-sparsity / KL penalties that sparsify marginals
  across the dataset, Top-k guarantees each input uses at most \(k\) hidden units.
- **Sparsity–locality trade-off:** large \(k\) → local stroke/edge filters (good for deep
  pretraining); medium \(k\) → more global parts (best for shallow classifiers); very small \(k\)
  → overly global features that stop factoring the input into parts.
- **Dead-unit scheduling:** starting from a large \(k\) and annealing to the target prevents early
  winner-take-all lock-in that would leave units untrained.
- **Encoding vs training support:** at test time, using \(\alpha k\) largest units (\(\alpha \ge 1\)
  chosen on validation) slightly improves classification over the training \(k\).

## Methodology

- **Architecture:** shallow AE with **linear** activations and **tied** weights
  \(P = W^\top\); optional bias for mean subtraction.
- **Train step:** compute \(z = W^\top x + b\); set \(z_{\Gamma^c} = 0\) for
  \(\Gamma = \mathrm{supp}_k(z)\); reconstruct \(\hat{x} = Wz + b'\); backprop MSE **only through
  the k active units**.
- **Sparse encoding (downstream):** features \(h = W^\top x + b\) with support
  \(\mathrm{supp}_{\alpha k}(h)\).
- **Analysis:** views training as a one-step approximation to iterative thresholding with
  inversion (ITI) sparse coding plus joint dictionary update; argues convergence implies a
  sufficiently **incoherent** dictionary (support recovery via \(\mathrm{supp}_k(W^\top x)\)).
- **Stacking:** greedy layer-wise k-sparse AE pretraining for deep nets; fine-tuning keeps the
  \(\alpha k\) Top-k nonlinearity.
- **Data:** MNIST, small NORB, and CIFAR-10 \(8\times 8\) patches (Gabor-like filters at
  \(k=50\)).

## Related

- extends [[2006-hinton-deep-autoencoder]] — same reconstructive AE skeleton, but replaces a
  compressive bottleneck + RBM pretraining with an overcomplete code regularized by hard Top-k
- background-for [[2023-bricken-towards-monosemanticity]] — supplies the hard k-sparse activation
  idea that later L1 SAEs revisit (Bricken uses soft L1+ReLU sparsity instead)
- introduces [[k-sparse-autoencoder]] — hard Top-k as the sole nonlinearity and exact \(L_0\)
  control
- applies [[sparse-autoencoder-dictionary-learning]] — AE-as-dictionary-learning with exact
  support selection rather than an L1 proxy
- background-for [[monosemantic-features-vs-polysemantic-neurons]] — sparsifying the code is
  motivated by part-based / invariant features, not yet by LM monosemanticity
- [[Sources MOC]]
- [[Autoencoder MOC]]
