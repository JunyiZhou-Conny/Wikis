---
title: "Improving and Generalizing Flow-Based Generative Models with Minibatch Optimal Transport"
type: source
status: done
date: 2026-07-14
source_kind: paper
tier: A
venue: "TMLR"
year: 2024
authors: ["Tong", "Fatras", "Malkin", "Huguet", "Zhang", "Rector-Brooks", "Wolf", "Bengio"]
approx_citations: 980
doi: "10.48550/arXiv.2302.00482"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/neural-ot
  - topic/wasserstein
  - method/neural-ot
---

# Improving and Generalizing Flow-Based Generative Models with Minibatch Optimal Transport

Tong, Fatras, Malkin, Huguet, Zhang, Rector-Brooks, Wolf & Bengio, *TMLR* 2024 (arXiv 2023).
The canonical **OT-CFM** paper: simulation-free continuous normalizing flows whose conditional
paths are built from (mini-batch) optimal-transport couplings — a bridge from static OT to
dynamic OT / Schrödinger bridges without integrating ODEs at train time.

## Summary

Continuous normalizing flows (CNFs) map a source density to a target by integrating a neural
ODE, but classical maximum-likelihood CNF training is simulation-heavy, and early flow-matching
objectives assumed a Gaussian source. This paper introduces **conditional flow matching (CFM)**:
a family of simulation-free regression objectives that fit a time-dependent vector field to
tractable *conditional* flows \(u_t(x\mid z)\) whose mixture recovers the desired marginal flow.
**Independent CFM (I-CFM)** couples unpaired \(x_0,x_1\) independently; **OT-CFM** instead samples
pairs from a (mini-batch) \(W_2\) plan \(\pi\), yielding straighter paths that approximate
**dynamic** OT as the conditional bandwidth \(\sigma\to 0\). An entropic variant **SB-CFM**
matches Schrödinger-bridge probability flows via entropy-regularized OT couplings. Experiments
cover low-dimensional OT fidelity, single-cell trajectory interpolation, CIFAR-10 generation,
and CelebA attribute translation; code ships as `torchcfm`.

## Key claims / results

- **CFM = FM in expectation:** under mild positivity, \(\nabla_\theta\mathcal{L}_{\mathrm{CFM}}=\nabla_\theta\mathcal{L}_{\mathrm{FM}}\)
  (Theorem 3.2), so one can regress against cheap conditional targets \(u_t(x\mid z)\) instead of
  the intractable marginal field.
- **I-CFM** handles arbitrary (non-Gaussian, density-free) sources by conditioning on independent
  pairs with linear interpolants \(\mu_t=tx_1+(1-t)x_0\) and constant velocity \(u_t=x_1-x_0\).
- **OT-CFM** sets \(q(z)=\pi(x_0,x_1)\) to a static \(W_2\) plan; as \(\sigma\to 0\), the induced
  marginal flow solves the Benamou–Brenier dynamic OT problem (Proposition 3.4). Mini-batch OT
  approximations still give correct generative models with only mild dynamic-OT degradation.
- **SB-CFM** uses the entropic plan \(\pi_{2\sigma^2}\) plus Brownian-bridge conditionals; the
  learned ODE matches Schrödinger-bridge marginals (Proposition 3.5). Limits recover OT-CFM
  (\(\varepsilon\to 0\)) and I-CFM (\(\varepsilon\to\infty\)).
- Empirically: lower normalized path energy vs prior neural OT / CNF baselines; faster training
  and fewer NFEs at matched sample quality; best average 1-Wasserstein on leave-one-out
  single-cell interpolation (CITE-seq, Multiome, embryoid body); CIFAR-10 FID competitive with
  improved FM training recipes, with OT-CFM strongest at low NFE.

## Methodology

- Draw \(t\sim U(0,1)\), condition \(z\) (independent pair, OT pair, or entropic pair), sample
  \(x\sim p_t(\cdot\mid z)\), regress \(v_\theta(t,x)\) onto \(u_t(x\mid z)\) with an \(L^2\) loss.
- For large data, recompute a mini-batch OT (or Sinkhorn) coupling each step between source and
  target mini-batches (Fatras-style), then sample pairs from that coupling.
- Inference: integrate the learned ODE with fixed-step Euler or adaptive (dopri5) solvers; no
  score network required for the deterministic OT-CFM / I-CFM flows.

## Related

- applies [[neural-optimal-transport]] — learns continuous OT / generative maps as CNF vector fields rather than dual potentials or maximin maps
- applies [[monge-kantorovich-formulations]] — lifts a static Kantorovich plan \(\pi\) to a dynamic probability flow
- applies [[wasserstein-distance]] — static \(W_2\) couplings and path-energy comparison to \(W_2^2\) for dynamic-OT fidelity
- applies [[entropic-regularization-sinkhorn]] — SB-CFM / mini-batch entropic plans reuse Sinkhorn couplings as CFM conditions
- extends [[2023-korotin-neural-optimal-transport]] — sibling neural OT solver; OT-CFM is simulation-free dynamic OT via flow matching vs Korotin's maximin dual for strong/weak costs
- benchmarks [[2023-bunne-cellot-neural-ot]] — both target single-cell transport; OT-CFM interpolates unpaired timepoints with CNFs, CellOT learns ICNN Monge maps for perturbations
- applies [[2013-cuturi-sinkhorn-distances]] — mini-batch / entropic OT plans that condition OT-CFM and SB-CFM
- background-for [[2000-benamou-dynamic-formulation]] — OT-CFM's limiting flow is the Benamou–Brenier dynamic formulation (draft sibling note)
- [[Sources MOC]]
- [[Optimal Transport MOC]]
