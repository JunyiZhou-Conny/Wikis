---
title: "Towards Monosemanticity: Decomposing Language Models With Dictionary Learning"
type: source
status: done
date: 2026-07-10
source_kind: paper
tier: A
venue: "Transformer Circuits Thread (Anthropic)"
year: 2023
authors: ["Bricken", "Templeton", "Batson", "Chen", "Jermyn", "Olah"]
approx_citations: 700
doi: ""
source_path: "sources/raw/sae/"
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/autoencoder
  - method/sparse-autoencoder
  - method/autoencoder
---

# Towards Monosemanticity: Decomposing Language Models With Dictionary Learning

Bricken, Templeton, Batson, Chen, Jermyn, Olah et al., *Transformer Circuits Thread* (Anthropic),
Oct 2023. Canonical **sparse autoencoder (SAE)** demonstration that dictionary learning can pull
**monosemantic features** out of polysemantic MLP neurons in a language model.

## Summary

Neurons in neural nets are often **polysemantic** — one unit fires for unrelated concepts — which
blocks mechanistic interpretability. The authors argue this is expected under **superposition**:
models pack more features than they have neurons into overlapping linear directions. They train a
**sparse autoencoder** (weak dictionary learning) on MLP activations of a one-layer transformer
(512 neurons) and recover an overcomplete set of features that are far more monosemantic than the
neuron basis, enabling inspection, steering, and basic circuit-style analysis.

## Key claims / results

- **SAEs extract relatively monosemantic features**, supported by hand case studies (Arabic script,
  DNA, base64, Hebrew), human ratings on random samples, and automated interpretability of
  activations and logit weights — most learned features look interpretable relative to neurons.
- Features can be **invisible in the neuron basis** (e.g. a Hebrew-script feature never dominates
  any neuron's top examples) yet still causal: pinning a feature steers generation (base64 →
  base64 text; Arabic → Arabic text).
- Features are **relatively universal** across two identically trained transformers (different
  seeds): SAE features match across models better than they match either model's neurons.
- **Feature splitting**: as dictionary width grows from 1× (512) to 256× (131,072), coarse
  features refine into families of finer, still-interpretable roles — different SAE sizes give
  different "resolutions."
- Just **512 neurons can represent tens of thousands of features**; features also compose into
  finite-state-automata-like systems (e.g. valid HTML generation).

## Methodology

- **Subject model:** one-layer transformer with a 512-unit ReLU MLP, trained on The Pile
  (~100B tokens); two seeds (A/B) for universality checks.
- **SAE architecture:** input bias → linear+bias+ReLU encoder → linear+bias decoder; trained with
  Adam on **MSE reconstruction + L1 sparsity** on the encoder activations.
- **Data scale:** ~8B MLP activation samples; expansion factors 1×–256×; detailed analysis on run
  **A/1** (4,096 features, 8×).
- **Dead-neuron resampling:** periodically reset encoder weights for units that stop firing so the
  dictionary keeps covering poorly reconstructed directions.
- Prefer SAEs over stronger classical dictionary-learning solvers so the decomposer is no more
  powerful than the MLP itself at recovering features from superposition.

## Related

- extends [[1997-olshausen-sparse-coding-overcomplete]] — classical overcomplete sparse coding, applied as an SAE on LM MLP activations
- extends [[2006-hinton-deep-autoencoder]] — keeps AE reconstruction, but replaces the compressive bottleneck with an **overcomplete sparse** code aimed at interpretability
- contrasts [[2013-kingma-vae]] — deterministic L1-sparse AE on frozen activations vs probabilistic ELBO latents trained end-to-end
- introduces [[sparse-autoencoder-dictionary-learning]] — SAE as scalable weak dictionary learning for superposition
- introduces [[monosemantic-features-vs-polysemantic-neurons]] — features (linear directions) as the right analysis unit over neurons
- contrasts [[passive-latent-dimensions]] — SAE L1 sparsity + dead-feature resampling vs VAE posterior collapse as two different "unused axis" stories
- [[Sources MOC]]
- [[Autoencoder MOC]]
