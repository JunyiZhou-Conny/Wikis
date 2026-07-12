---
title: "Neural Optimal Transport"
type: source
status: done
date: 2026-07-10
source_kind: paper
tier: A
venue: "ICLR 2023"
year: 2023
authors: ["Korotin", "Selikhanovych", "Burnaev"]
approx_citations: 140
doi: "10.48550/arXiv.2201.12220"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/neural-ot
  - topic/wasserstein
  - method/neural-ot
---

# Neural Optimal Transport

Korotin, Selikhanovych & Burnaev, *ICLR 2023* (spotlight). A general **neural solver for OT
maps and plans** under strong and weak costs — the method-level counterpart to applied neural OT
like CellOT.

## Summary

Most scalable neural OT work either estimates only the OT *cost* (WGANs) or recovers a
*deterministic* map for quadratic cost (ICNN / maximin dual methods). This paper learns a
parameterized **stochastic transport map** \(T(x,z)\) that can represent nondeterministic plans,
via a maximin reformulation of the dual for **weak** OT costs (Gozlan et al.). Strong costs and
deterministic maps fall out as special cases. They prove neural nets are universal approximators
of stochastic transport maps, and demonstrate unpaired image-to-image translation (one-to-one and
one-to-many) with a single \(\gamma\) knob controlling conditional diversity.

## Key claims / results

- Dual weak-OT cost admits a **maximin** form \(\sup_f \inf_T \mathcal{L}(f,T)\) where \(T\) is a
  stochastic map \(T:\mathcal{X}\times\mathcal{Z}\to\mathcal{Y}\) (noise outsourcing); optimal
  \(T^*\) realizes an OT plan.
- Algorithm (NOT): SGAD on networks \(f_\omega\) and \(T_\theta\); Monte-Carlo estimators for strong
  costs and for the \(\gamma\)-weak quadratic cost \(\mathcal{W}_{2,\gamma}\).
- For strong quadratic cost (\(\gamma=0\)), \(T(x,z)\) **conditionally collapses** to a deterministic
  map (recovering prior maximin / MM:R solvers); for \(\gamma>0\), conditional variance is
  encouraged and one-to-many maps stay stochastic.
- Theorem: under mild conditions, neural nets densely approximate stochastic transport maps in
  \(L^2\) while keeping the pushforward \(\varepsilon\)-close in \(\mathbb{W}_2^2\).
- Unpaired translation on CelebA / anime / shoes / handbags / LSUN churches preserves input
  attributes under \(L^2\) pixel cost; \(\gamma\) trades sample diversity vs. input similarity.
- Limitation: not every saddle \(T^*\) is guaranteed to be an OT map; saddle geometry and
  \(\operatorname{arg\,inf}\) sets remain open.

## Methodology

- Start from weak OT (cost \(C(x,\mu)\) on a point and a conditional measure); dual via weak
  \(C\)-transform.
- Reformulate the \(C\)-transform by pushing an atomless noise \(\mathbb{S}\) through maps
  \(t:\mathcal{Z}\to\mathcal{Y}\), then interchange inf and integral (Rockafellar) to get a joint
  map \(T(x,z)\).
- Train with \(K_T>1\) inner steps on \(T\) per outer step on \(f\) (opposite the usual GAN schedule);
  no Lipschitz constraint on \(f\).
- Empirically: U-Net-style \(T\), ResNet potential \(f\); strong \(\mathbb{W}_2\) for one-to-one,
  \(\mathcal{W}_{2,\gamma}\) (\(\gamma\in\{\tfrac{2}{3},1\}\)) for one-to-many.

## Related

- introduces [[neural-optimal-transport]] — general maximin neural solver for strong/weak OT plans
- applies [[monge-kantorovich-formulations]] — dual weak/strong OT; stochastic maps realize Kantorovich plans
- background-for [[wasserstein-distance]] — \(\mathbb{W}_2\) and \(\gamma\)-weak quadratic costs as the working geometry
- extends [[2023-bunne-cellot-neural-ot]] — method-level neural OT (stochastic plans, weak costs) vs CellOT's ICNN Monge maps for single-cell
- benchmarks [[2019-yang-scalable-unbalanced-ot-gans]] — sibling neural transport-map learner; NOT targets balanced weak/strong OT rather than unbalanced mass scaling
- contrasts [[2023-shi-diffusion-schrodinger-bridge-matching]] — static strong/weak neural plans vs DSBM’s dynamic entropic path measures
- [[Sources MOC]]
- [[Optimal Transport MOC]]
