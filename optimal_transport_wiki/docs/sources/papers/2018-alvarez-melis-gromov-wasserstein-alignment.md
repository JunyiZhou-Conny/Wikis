---
title: "Gromov-Wasserstein Alignment of Word Embedding Spaces"
type: source
status: done
date: 2026-07-07
source_kind: paper
tier: A
venue: "EMNLP 2018"
year: 2018
authors: ["Alvarez-Melis", "Jaakkola"]
approx_citations: 400
doi: "10.48550/arXiv.1809.00013"
source_path: "sources/raw/alvarez-melis-2018-gw.pdf"
tags:
  - source
  - domain/ml
  - domain/literature
  - field/nlp
  - topic/gromov-wasserstein
  - method/gromov-wasserstein
  - method/sinkhorn
---

# Gromov-Wasserstein Alignment of Word Embedding Spaces

Alvarez-Melis & Jaakkola, *EMNLP 2018*. Casts unsupervised cross-lingual word alignment as a
**Gromov-Wasserstein** OT problem — a clean applied entry point to relational OT. (Provided by
user.)

## Summary

Classic OT needs a cost between points **across** the two domains, which is unavailable for
independently-trained monolingual word embeddings (they are only defined up to rotation). The
paper instead uses the **Gromov-Wasserstein (GW) distance**, which compares **intra-domain**
pairwise similarity matrices, so it operates on *distances between distances* and needs no shared
metric space. Solving GW yields a soft coupling Γ that directly gives (probabilistic) word
translations, with no post-hoc heuristics.

## Key claims / results

- GW alignment is fully unsupervised, single-step, and needs little/no tuning; the coupling Γ*
  *is* the translation, avoiding nearest-neighbor hubness fixes (CSLS, inverted softmax).
- Matches near state-of-the-art on benchmark bilingual lexicon induction (Conneau 2018, Dinu
  2014) at a fraction of the compute (CPU minutes vs GPU).
- Optimized via projected gradient descent where **each iteration is an entropic OT problem**
  solved with **Sinkhorn** (Cuturi 2013); Peyré et al. 2016 reduce the naive 4th-order-tensor
  cost.
- For large vocabularies, a two-step scheme learns an explicit orthogonal (Procrustes) map from
  the GW coupling.
- The optimal GW value is itself a **distance between languages** (Mémoli 2011).

## Methodology

- Discrete Kantorovich couplings over the polytope Π(p, q); GW objective is quadratic
  (non-convex) in Γ.
- Cosine intra-domain similarity + L2 loss between similarities; entropic regularization λ tuned
  only via cost-matrix normalization.

## Related

- introduces [[gromov-wasserstein-distance]] — relational OT across incomparable metric spaces
- applies [[entropic-regularization-sinkhorn]] — each GW iteration is a Sinkhorn OT solve
- background-for [[monge-kantorovich-formulations]] — builds on the Kantorovich coupling polytope
- extends [[2011-memoli-gromov-wasserstein]] — applies Mémoli's GW metric to bilingual lexicon induction
- extends [[2013-cuturi-sinkhorn-distances]] — uses entropic OT as the inner solver
- benchmarks [[2023-bunne-cellot-neural-ot]] — sibling applied-OT source (biology vs NLP)
- [[Sources MOC]]
- [[Optimal Transport MOC]]
