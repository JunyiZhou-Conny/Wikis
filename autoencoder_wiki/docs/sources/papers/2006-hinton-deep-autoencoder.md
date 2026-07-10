---
title: "Reducing the Dimensionality of Data with Neural Networks (deep autoencoder)"
type: source
status: done
date: 2026-07-07
source_kind: paper
tier: A
venue: "Science"
year: 2006
authors: ["Hinton", "Salakhutdinov"]
approx_citations: 22000
doi: "10.1126/science.1127647"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/autoencoder
  - topic/dimensionality-reduction
  - method/autoencoder
  - method/rbm-pretraining
---

# Reducing the Dimensionality of Data with Neural Networks (deep autoencoder)

Hinton & Salakhutdinov, *Science* 2006. The **canonical deep autoencoder paper** — establishes
the encoder/decoder/bottleneck architecture for nonlinear dimensionality reduction and shows it
beats PCA. This is the general-autoencoder root the wiki's applied VAE work sits on top of.

## Summary

A multilayer neural network with a small central "code" layer is trained to reconstruct its
high-dimensional input; the low-dimensional central layer becomes a nonlinear code. The paper's
key contribution is a **layer-wise pretraining** scheme (stacked Restricted Boltzmann Machines)
that initializes the weights close to a good solution, making deep autoencoders trainable by
backpropagation where naive initialization fails. The learned codes outperform **PCA** on
reconstruction and downstream visualization/classification.

## Key claims / results

- Deep **autoencoders** learn nonlinear low-dimensional codes that beat **PCA** on reconstruction.
- Naive gradient descent fails for deep autoencoders; **good weight initialization is essential**
  (large weights → poor local minima; small weights → vanishing gradients in early layers).
- **RBM pretraining** then fine-tuning solves the initialization problem.

## Methodology

- **Architecture:** symmetric encoder → central code layer (bottleneck) → decoder.
- **Objective:** minimize reconstruction error between input and its reconstruction.
- **Training:** greedy layer-wise RBM pretraining, then joint fine-tuning via backprop.
- Demonstrated on images and documents.

## Related

<Typed links — this is the general-AE root the VAE thread and DR work descend from.>

- background-for [[2013-kingma-vae]] — the VAE adds a probabilistic latent + ELBO on top of this encoder/decoder/bottleneck idea
- background-for [[2020-li-dr-benchmark]] — establishes the "nonlinear AE vs PCA" comparison this benchmark later runs at scale on scRNA
- introduces [[vae-vs-linear-nonlinear-dr-benchmarks]] — the original "autoencoder beats linear DR" result
- background-for [[scrna-dr-pipeline-hvg-to-latent]] — the encoder → latent code pattern that pipeline instantiates
- background-for [[2023-bricken-towards-monosemanticity]] — SAE reuses AE reconstruction but targets overcomplete sparse features, not a compressive bottleneck
- background-for [[sparse-autoencoder-dictionary-learning]] — the reconstructive AE skeleton SAEs inherit and invert (expand + sparsify)
- background-for [[monosemantic-features-vs-polysemantic-neurons]] — useful codes ≠ monosemantic neuron axes
- [[Sources MOC]]
- [[Autoencoder MOC]]
