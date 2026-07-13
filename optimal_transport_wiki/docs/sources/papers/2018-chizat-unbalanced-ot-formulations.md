---
title: "Unbalanced Optimal Transport: Dynamic and Kantorovich Formulations"
type: source
status: done
date: 2026-07-07
source_kind: paper
tier: A
venue: "Journal of Functional Analysis"
year: 2018
authors: ["Chizat", "Peyré", "Schmitzer", "Vialard"]
approx_citations: 200
doi: "10.1016/j.jfa.2018.03.008"
source_path: "sources/raw/chizat-2018-unbalanced-formulations.pdf"
tags:
  - source
  - domain/math
  - domain/literature
  - topic/unbalanced-ot
  - method/unbalanced-ot
---

# Unbalanced Optimal Transport: Dynamic and Kantorovich Formulations

Chizat, Peyré, Schmitzer & Vialard, *J. Functional Analysis* 2018. The theoretical foundation of
**unbalanced** optimal transport — OT between measures of *different total mass*.

## Summary

Classical OT requires the two measures to have equal mass (probability distributions). This paper
defines a class of distances between **arbitrary nonnegative Radon measures** via two equivalent
convex formulations: (i) a **dynamic** geodesic formulation over the space of measures, and (ii)
a **static Kantorovich** formulation minimizing over couplings that describe transport **plus
creation and destruction** of mass. Being able to switch formulations per application is the key
contribution. The **Wasserstein-Fisher-Rao** (WFR) metric is a distinguished member.

## Key claims / results

- Extends OT to unequal-mass measures by **relaxing the hard marginal constraints**, penalizing
  marginal deviation (e.g. via KL / Fisher-Rao terms) instead of enforcing exact matching.
- Dynamic and static formulations are **equivalent convex problems**; each is preferable for
  different tasks (geodesics vs couplings).
- Recovers the **Wasserstein-Fisher-Rao / Hellinger-Kantorovich** metric, unifying independent
  constructions (Chizat et al.; Kondratyev et al.; Liero et al.).

## Methodology

- Convex analysis over measures; dynamic (Benamou-Brenier-type) and static Kantorovich duality.

## Related

- introduces [[balanced-vs-unbalanced-ot]] — defines the unbalanced problem via marginal relaxation
- introduces [[wasserstein-fisher-rao-metric]] — defines this distinguished metric as a special member
- extends [[monge-kantorovich-formulations]] — generalizes the Kantorovich coupling to unequal mass
- extends [[2000-benamou-dynamic-formulation]] — lifts the Benamou–Brenier dynamic action to unequal-mass measures
- extends [[benamou-brenier-formulation]] — dynamic unbalanced OT is the continuity-equation template plus growth
- background-for [[2018-chizat-scaling-algorithms-unbalanced]] — the theory its scaling algorithms solve
- background-for [[2019-sejourne-unbalanced-sinkhorn-divergences]] — formal basis for unbalanced Sinkhorn divergences
- [[Sources MOC]]
- [[Optimal Transport MOC]]
