---
title: "Sinkhorn Divergences for Unbalanced Optimal Transport"
type: source
status: done
date: 2026-07-07
source_kind: paper
tier: C
venue: "arXiv (preprint)"
year: 2019
authors: ["Séjourné", "Feydy", "Vialard", "Trouvé", "Peyré"]
approx_citations: 25
doi: "10.48550/arXiv.1910.12958"
source_path: "sources/raw/sejourne-2019-unbalanced-sinkhorn.pdf"
tags:
  - source
  - domain/ml
  - domain/math
  - domain/literature
  - topic/unbalanced-ot
  - method/sinkhorn
  - method/unbalanced-ot
---

# Sinkhorn Divergences for Unbalanced Optimal Transport

Séjourné, Feydy, Vialard, Trouvé & Peyré, *arXiv 2019*. **Tier C — preprint; flagged per vault
contract.** Makes unbalanced entropic OT into a well-behaved, debiased loss.

## Summary

Entropic (Sinkhorn) OT is **biased**: it does not vanish when the two measures are equal, and it
blurs the transport plan. The paper extends the **Sinkhorn divergence** debiasing —
S(α,β) = OTε(α,β) − ½OTε(α,α) − ½OTε(β,β) — to the **unbalanced** setting, where marginals are
relaxed via divergence penalties. The result is a class of losses that are positive, definite,
metrize convergence, and are robust to mass variation and outliers, while remaining
Sinkhorn-cheap.

## Key claims / results

- Defines **unbalanced Sinkhorn divergences** that interpolate between OT and MMD-type behaviors
  and remove the entropic bias in the unequal-mass setting.
- Establishes positivity/definiteness and favorable geometric properties.
- Robust to outliers and mass fluctuations — attractive as a differentiable ML loss.
- Tier C: influential arXiv preprint by leading OT authors, but flagged as not formally
  peer-reviewed in this record.

## Methodology

- Debiased entropic objective with KL-type marginal relaxations; Sinkhorn-style iterations.

## Related

- extends [[2018-chizat-scaling-algorithms-unbalanced]] — debiases the unbalanced Sinkhorn costs it computes
- applies [[entropic-regularization-sinkhorn]] — corrects the entropic bias of Sinkhorn in the unbalanced case
- background-for [[balanced-vs-unbalanced-ot]] — a practical loss for the unbalanced regime
- extends [[2018-chizat-unbalanced-ot-formulations]] — builds losses on that formulation's marginal relaxation
- [[Sources MOC]]
- [[Optimal Transport MOC]]
