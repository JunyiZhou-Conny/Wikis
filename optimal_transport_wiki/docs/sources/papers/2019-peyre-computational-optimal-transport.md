---
title: "Computational Optimal Transport"
type: source
status: done
date: 2026-07-07
source_kind: book
tier: A
venue: "Foundations and Trends in Machine Learning"
year: 2019
authors: ["Peyré", "Cuturi"]
approx_citations: 5400
doi: "10.1561/2200000073"
source_path: "sources/raw/peyre-cuturi-2019-comput-ot.pdf"
tags:
  - source
  - domain/ml
  - domain/math
  - domain/literature
  - topic/wasserstein
  - method/sinkhorn
---

# Computational Optimal Transport

Peyré & Cuturi, *Foundations and Trends in ML* 2019. The standard reference monograph tying
together OT theory and the algorithms used across this wiki.

## Summary

A comprehensive, ML-oriented survey of **computational** optimal transport: Monge and
Kantorovich formulations, the dual, the Wasserstein distances, entropic regularization and the
Sinkhorn algorithm, Wasserstein barycenters, Gromov-Wasserstein, and extensions including
**unbalanced** and dynamic OT. It is the connective reference for the specialized papers here.

## Key claims / results

- Presents OT as a unified toolbox for comparing and coupling probability distributions.
- Systematizes **entropic regularization** as the workhorse for scalable OT and derives Sinkhorn
  convergence / stability.
- Surveys **Gromov-Wasserstein**, barycenters, and **unbalanced OT** as principled extensions
  beyond the mass-conserving, same-space setting.

## Methodology

- Expository/monograph: definitions, duality, algorithms, and worked ML applications.

## Related

- extends [[2013-cuturi-sinkhorn-distances]] — systematizes the entropic/Sinkhorn method it helped popularize
- introduces [[wasserstein-distance]] — canonical reference definition used across the wiki
- background-for [[monge-kantorovich-formulations]] — textbook treatment of primal/dual OT
- background-for [[gromov-wasserstein-distance]] — surveys GW among OT extensions
- background-for [[balanced-vs-unbalanced-ot]] — situates unbalanced OT within computational OT
- background-for [[schrodinger-bridge]] — surveys entropic / dynamic OT that SBs instantiate
- background-for [[2023-shi-diffusion-schrodinger-bridge-matching]] — EOT monograph backdrop for DSBM
- [[Sources MOC]]
- [[Optimal Transport MOC]]
