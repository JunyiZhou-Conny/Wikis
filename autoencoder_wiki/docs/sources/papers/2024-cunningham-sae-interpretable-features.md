---
title: "Sparse Autoencoders Find Highly Interpretable Features in Language Models"
type: source
status: done
date: 2026-07-13
source_kind: paper
tier: A
venue: "ICLR"
year: 2024
authors: ["Cunningham", "Ewart", "Riggs", "Huben", "Sharkey"]
approx_citations: 800
doi: "10.48550/arXiv.2309.08600"
source_path: "sources/raw/sae/"
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/autoencoder
  - method/sparse-autoencoder
  - method/autoencoder
---

# Sparse Autoencoders Find Highly Interpretable Features in Language Models

Cunningham, Ewart, Riggs, Huben, Sharkey, *ICLR* 2024 (arXiv:2309.08600). Peer-reviewed
**sparse autoencoder (SAE)** demonstration that overcomplete L1-sparse dictionaries recover
interpretable, causally useful features from language-model activations (mainly residual streams
of Pythia-70M/410M).

## Summary

Polysemantic neurons and residual-stream directions block mechanistic interpretability when models
store more features than dimensions (**superposition**). The authors train tied-weight ReLU sparse
autoencoders on frozen LM activations so each activation is a sparse linear combination of learned
dictionary atoms. Relative to the neuron basis, random directions, PCA, and ICA, SAE features
score higher on automated interpretability (Bills et al.), localize IOI behaviour with fewer /
smaller activation patches, and support monosemantic case studies plus cross-layer circuit trees.

## Key claims / results

- **SAE dictionary features beat standard decompositions on autointerpretability** (top-and-random
  scores), especially in early residual-stream layers; the gap shrinks in later layers under fixed
  sparsity/expansion hyperparameters.
- **Causal localisation on IOI:** patching a small ACDC-ordered set of SAE features closes KL to a
  counterfactual target with fewer edits and smaller edit magnitude than PCA or a non-sparse
  (α = 0) autoencoder; higher α improves localisation but raises residual unexplained variance.
- **Monosemantic case studies:** features that fire on specific punctuation/contexts (e.g. apostrophe
  subtypes) have intuitive logit effects when ablated, and upstream SAE features form sparse causal
  trees toward output-aligned features (e.g. closing parentheses).
- **Scalable unsupervised method:** only unlabeled activations needed; compute far below pretraining;
  reconstruction–sparsity Pareto frontier remains a practical limiter.

## Methodology

- **Subject models / sites:** Pythia-70M and Pythia-410M residual streams (primary); also MLP /
  attention sublayers with mixed success.
- **SAE:** single hidden layer, expansion ratio R (dictionary size / `din`), **tied** encoder–decoder
  weights with row-normalized dictionary, ReLU encoder, bias; loss = normalized MSE reconstruction
  + α‖c‖₁ on codes.
- **Evaluation:** GPT-4 autointerpretability vs baselines; ACDC-guided activation patching on IOI;
  hand analysis of activating tokens, logit ablation, and recursive upstream ablation for circuits.
- Builds on Sharkey et al. (2023) sparse-coding-out-of-superposition agenda; concurrent in spirit
  with Anthropic's SAE thread.

## Related

- benchmarks [[2023-bricken-towards-monosemanticity]] — independent peer-reviewed SAE on Pythia residual streams (autointerp + IOI patching) vs Anthropic MLP SAE case studies
- extends [[2006-hinton-deep-autoencoder]] — same reconstructive AE skeleton, but overcomplete + L1-sparse codes aimed at interpretability rather than a compressive bottleneck
- contrasts [[2013-kingma-vae]] — deterministic L1-sparse AE on frozen LM activations vs probabilistic ELBO latents trained end-to-end
- applies [[sparse-autoencoder-dictionary-learning]] — tied ReLU SAE as scalable weak dictionary learning for superposition
- applies [[monosemantic-features-vs-polysemantic-neurons]] — autointerp, patching, and case studies as evidence that features beat the neuron basis
- [[Sources MOC]]
- [[Autoencoder MOC]]
