---
title: Optimal Transport MOC
type: moc
tags:
  - moc
  - domain/ml
  - domain/math
---

# Optimal Transport MOC

Topic index for optimal transport: from Monge/Kantorovich foundations to neural and
**unbalanced** OT.

## Start here (tutorials)

- [[2020-williams-intro-optimal-transport]] — intuition-first intro: Wasserstein vs KL, discrete OT as an LP, entropic reg. **Tier C (expository blog)**.

## Foundations

- [[2000-benamou-dynamic-formulation]] — dynamic / fluid-mechanics formulation of $W_2$ + ALG2 solver (Numerische Mathematik 2000). Tier A. Canonical Benamou–Brenier paper.
- [[2013-cuturi-sinkhorn-distances]] — entropic regularization + Sinkhorn scaling (NeurIPS 2013). Tier A. The computational root of modern OT.
- [[2019-peyre-computational-optimal-transport]] — the standard computational-OT monograph (Peyré & Cuturi). Tier A.

## Distances & couplings

- [[2018-alvarez-melis-gromov-wasserstein-alignment]] — Gromov-Wasserstein for aligning incomparable spaces (EMNLP 2018). Tier A.

## Neural / large-scale OT

- [[2023-korotin-neural-optimal-transport]] — Neural OT: maximin dual solver for strong/weak costs and stochastic plans (ICLR 2023 spotlight). Tier A.
- [[2023-bunne-cellot-neural-ot]] — CellOT: neural OT via input-convex nets for single-cell perturbations (Nature Methods 2023). Tier A.
- [[2019-yang-scalable-unbalanced-ot-gans]] — unbalanced OT via a GAN-style transport map + scaling factor (ICLR 2019). Tier A.

## Unbalanced OT (mass creation / destruction)

- [[2018-chizat-unbalanced-ot-formulations]] — dynamic & Kantorovich formulations for arbitrary positive measures (J. Functional Analysis 2018). Tier A. Theory root.
- [[2018-chizat-scaling-algorithms-unbalanced]] — Sinkhorn-type scaling algorithms for unbalanced OT (Mathematics of Computation 2018). Tier A.
- [[2019-sejourne-unbalanced-sinkhorn-divergences]] — debiased Sinkhorn divergences for the unbalanced setting. **Tier C (preprint)**.

## Concepts

- [[monge-kantorovich-formulations]]
- [[wasserstein-distance]]
- [[benamou-brenier-formulation]]
- [[entropic-regularization-sinkhorn]]
- [[gromov-wasserstein-distance]]
- [[balanced-vs-unbalanced-ot]]
- [[wasserstein-fisher-rao-metric]]
- [[neural-optimal-transport]]

## All sources

```dataview
TABLE tier, venue, year, approx_citations AS cites
FROM "sources"
WHERE type = "source" AND source_kind = "paper"
SORT tier ASC, year ASC
```

## All concepts

```dataview
TABLE status, date, length(distilled_from) AS "From N sources"
FROM "concepts"
WHERE type = "concept"
SORT file.name ASC
```

## Related

- [[Home MOC]]
- [[Sources MOC]]
