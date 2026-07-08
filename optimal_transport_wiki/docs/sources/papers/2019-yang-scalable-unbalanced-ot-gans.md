---
title: "Scalable Unbalanced Optimal Transport using Generative Adversarial Networks"
type: source
status: done
date: 2026-07-07
source_kind: paper
tier: A
venue: "ICLR 2019"
year: 2019
authors: ["Yang", "Uhler"]
approx_citations: 120
doi: "10.48550/arXiv.1810.11447"
source_path: "sources/raw/yang-uhler-2019-uot-gans.pdf"
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/unbalanced-ot
  - topic/neural-ot
  - method/neural-ot
  - method/gan
---

# Scalable Unbalanced Optimal Transport using Generative Adversarial Networks

Yang & Uhler, *ICLR 2019*. Brings **unbalanced** OT to high-dimensional continuous measures with
a GAN-style neural solver — the neural bridge between unbalanced OT theory and applications.

## Summary

Formulates unbalanced OT as **simultaneously learning a transport map T and a scaling factor ξ**
that push a source measure toward a target in a cost-optimal way, allowing mass to be created or
destroyed (the ξ reweights mass). Both are parameterized by neural networks and trained with
**stochastic alternating gradient updates**, in practice resembling GAN training, which scales to
high-dimensional continuous distributions where discrete solvers cannot.

## Key claims / results

- Casts unbalanced OT as a saddle-point problem solvable with GAN-like alternating updates.
- Shows the formulation is **closely related to the static unbalanced OT of Liero et al. (2018)**,
  giving it theoretical grounding.
- Scales to high-dimensional continuous measures; demonstrated on **population modeling**.
- ICLR is a top venue → Tier A, though the transport/scaling factorization is only practical in
  its full form for moderate settings.

## Methodology

- Neural transport map + scaling factor; adversarial (min–max) optimization over the dual.

## Related

- introduces [[balanced-vs-unbalanced-ot]] — learns a scaling factor to allow mass creation/destruction
- applies [[neural-optimal-transport]] — a GAN-style neural solver for OT maps
- benchmarks [[2023-bunne-cellot-neural-ot]] — sibling neural-OT method (ICNN dual vs GAN saddle point)
- extends [[2018-chizat-unbalanced-ot-formulations]] — neural realization related to static unbalanced OT
- [[Sources MOC]]
- [[Optimal Transport MOC]]
