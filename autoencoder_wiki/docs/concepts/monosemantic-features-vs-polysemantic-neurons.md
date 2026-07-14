---
title: Monosemantic features vs polysemantic neurons
type: concept
status: done
date: 2026-07-10
tags:
  - concept
  - domain/ml
  - topic/autoencoder
  - method/sparse-autoencoder
distilled_from:
  - "[[2023-bricken-towards-monosemanticity]]"
  - "[[2006-hinton-deep-autoencoder]]"
---

# Monosemantic features vs polysemantic neurons

A **polysemantic neuron** responds to a jumble of unrelated inputs; a **monosemantic feature** is
a direction (often a sparse dictionary atom) that tracks one coherent concept. When models use
**superposition**, the neuron basis is the wrong unit of analysis — features are.

## Why it matters / where it shows up

Autoencoders and MLPs give you a coordinate basis (hidden units / code dims), but that basis need
not align with human-meaningful factors ([[2006-hinton-deep-autoencoder]] gives useful codes, not
guaranteed monosemantic axes). Interpretability work therefore *re-decomposes* activations into
features ([[2023-bricken-towards-monosemanticity]]).

## Details

- **Polysemanticity:** one neuron mixes unrelated contexts (e.g. citations + dialogue + HTTP +
  Korean in a small LM); also classic in vision (cat faces + car fronts).
- **Superposition hypothesis:** more useful sparse features than neurons → features stored as
  overlapping linear combinations; sparsity at inference lets the net (and an SAE) disentangle them.
- **Evidence a feature is "real":** consistent activating examples, causal steering when pinned,
  presence across models (universality), and absence from any single neuron's top examples.
- **Not the same as VAE "passive dims":** unused VAE axes collapse to the prior
  ([[passive-latent-dimensions]]); polysemantic neurons are *used* but *mixed*.

## Related

- introduces [[2023-bricken-towards-monosemanticity]] — SAEs as a practical route to monosemantic features in LM MLPs
- background-for [[2006-hinton-deep-autoencoder]] — bottleneck codes are useful representations, not a claim of monosemantic neurons
- applies [[sparse-autoencoder-dictionary-learning]] — the decomposition method that targets this distinction
- contrasts [[passive-latent-dimensions]] — mixed-but-active neurons vs collapsed unused latent axes
- contrasts [[2017-higgins-beta-vae]] — post-hoc SAE features for superposition vs end-to-end β-VAE factor latents
- contrasts [[beta-vae-weighted-kl-disentanglement]] — monosemantic dictionary atoms vs β-weighted generative-factor codes
