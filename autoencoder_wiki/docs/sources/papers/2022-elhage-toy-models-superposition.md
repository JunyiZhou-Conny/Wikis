---
title: "Toy Models of Superposition"
type: source
status: done
date: 2026-07-11
source_kind: paper
tier: A
venue: "Transformer Circuits Thread (Anthropic)"
year: 2022
authors: ["Elhage", "Hume", "Olsson", "Schiefer", "Henighan", "Kravec", "Hatfield-Dodds", "Lasenby", "Drain", "Chen", "Grosse", "McCandlish", "Kaplan", "Amodei", "Wattenberg", "Olah"]
approx_citations: 680
doi: "10.48550/arXiv.2209.10652"
source_path: "sources/raw/sae/"
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/autoencoder
  - method/sparse-autoencoder
  - method/autoencoder
---

# Toy Models of Superposition

Elhage, Hume, Olsson, Schiefer, Henighan, Kravec, Hatfield-Dodds, Lasenby, Drain, Chen,
Grosse, McCandlish, Kaplan, Amodei, Wattenberg, Olah et al., *Transformer Circuits Thread*
(Anthropic), Sept 2022. Canonical toy-model demonstration that neural nets store **more
features than dimensions** via **superposition**, explaining polysemantic neurons.

## Summary

Neurons often fail to map cleanly to human-interpretable concepts (**polysemanticity**). This
paper trains tiny ReLU networks on synthetic sparse features to show when and why models pack
extra features into overlapping almost-orthogonal directions — **superposition** — trading
interference for capacity beyond a linear/PCA baseline. Nonlinear filtering (ReLU + bias) makes
that trade-off workable. The authors argue real nets may be noisily simulating larger sparse
feature models, and that this geometry is the right background for mechanistic interpretability.

## Key claims / results

- **Superposition is observed**, not just hypothesized: with sparse features, a low-dimensional
  ReLU bottleneck reconstructs more features than it has dimensions; a matched **linear** model
  only keeps the top principal components.
- **Monosemantic and polysemantic neurons both arise**, governed by a **phase change** in
  sparsity / importance — dense regimes look PCA-like; sparse regimes pack extra features with
  interference.
- Superposed features organize into **geometric structures** (digons, triangles, pentagons,
  tetrahedra / uniform polytopes) rather than arbitrary directions.
- Limited **computation in superposition** is possible (e.g. absolute-value circuits), supporting
  the “noisy simulation of a larger sparse net” picture.
- Preliminary links to **adversarial examples**, **grokking**, and mixture-of-experts style
  capacity; the toy system also shows rich training dynamics (energy-level-like jumps).

## Methodology

- **Synthetic features** \(x \in \mathbb{R}^n\): each coordinate is an idealized feature with
  sparsity \(S\) (often zero) and importance weight \(I_i\); nonzero draws are uniform on
  \([0,1]\).
- **Models:** linear baseline \(x' = W^\top W x + b\) vs **ReLU output**
  \(x' = \mathrm{ReLU}(W^\top W x + b)\), with \(h = Wx\) the low-dimensional code
  (\(m \ll n\)). Columns of \(W\) are feature directions.
- **Loss:** importance-weighted MSE \(\sum_i I_i (x_i - x'_i)^2\).
- Sweep sparsity, importance curves, and \(n/m\) to map the **superposition phase diagram** and
  visualize feature geometries; follow-on toys study privileged bases and computation under
  interference.

## Related

- background-for [[2023-bricken-towards-monosemanticity]] — supplies the superposition /
  polysemanticity theory that Bricken’s SAEs aim to unfold in real LM MLPs
- contrasts [[2006-hinton-deep-autoencoder]] — bottleneck AEs compress; superposition is
  overcomplete packing *inside* a narrow activation space, not a deeper stack
- contrasts [[linear-autoencoder-pca-equivalence]] — linear reconstruction recovers PCA-like
  top features; ReLU + sparsity enables capacity beyond that linear ceiling
- introduces [[monosemantic-features-vs-polysemantic-neurons]] — phase diagram for when neurons
  stay monosemantic vs mix unrelated features
- background-for [[sparse-autoencoder-dictionary-learning]] — motivates overcomplete sparse
  dictionaries as a way to recover features hidden in superposition
- [[Sources MOC]]
- [[Autoencoder MOC]]
