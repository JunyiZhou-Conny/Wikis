---
title: "Wasserstein Generative Adversarial Networks"
type: source
status: done
date: 2026-07-16
source_kind: paper
tier: A
venue: "ICML 2017"
year: 2017
authors: ["Arjovsky", "Chintala", "Bottou"]
approx_citations: 5000
doi: "10.48550/arXiv.1701.07875"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/wasserstein
  - topic/neural-ot
  - method/neural-ot
---

# Wasserstein Generative Adversarial Networks

Arjovsky, Chintala & Bottou, *ICML 2017* (FAIR). The paper that put the **Earth Mover /
Wasserstein-1** distance at the center of adversarial generative modeling — the classic ML
entry point for Wasserstein geometry.

## Summary

Standard GANs minimize (a surrogate of) Jensen–Shannon divergence. When data and model live on
low-dimensional manifolds with little overlap, JS/KL/TV yield discontinuous or saturated losses
and vanishing gradients. WGAN instead targets the **Wasserstein-1 (Earth Mover)** distance,
which metrizes weak convergence and stays continuous (and a.e. differentiable) under mild
conditions on the generator. Practically, they optimize the **Kantorovich–Rubinstein dual** with
a weight-clipped neural *critic*, producing a meaningful loss curve that correlates with sample
quality and much more stable training than JS-GANs.

## Key claims / results

- On disjoint / manifold-supported distributions, \(W_1\) can stay continuous in generator
  parameters while JS, KL, and TV jump or become infinite (parallel-lines example).
- Topology: KL ⇒ JS/TV ⇒ \(W_1\) (weakest among these); \(W_1\to 0\) iff convergence in
  distribution on compact spaces.
- **WGAN:** maximize \(E_{x\sim P_r}[f_w(x)] - E_z[f_w(g_\theta(z))]\) over \(K\)-Lipschitz
  critics \(f_w\) (enforced by clipping \(w\) to \([-c,c]\)), then descend on the generator;
  under optimality, \(\nabla_\theta W \approx -E_z[\nabla_\theta f_w(g_\theta(z))]\).
- Empirically: fewer mode collapses on Gaussian mixtures; critic loss tracks sample quality on
  LSUN bedrooms; training survives weaker architectures (no batch-norm, plain MLP generators)
  where standard GANs fail.
- Cost-only: recovers an estimate of the OT *distance*, not an explicit transport map/plan —
  the limitation later neural-OT solvers address.

## Methodology

- Start from Kantorovich \(W_1\) primal; switch to KR dual \(\sup_{\|f\|_L\le 1} E_{P_r}f - E_{P_\theta}f\).
- Parameterize critic by a neural net with compact weight box (clipping ⇒ uniform Lipschitz).
- Algorithm: \(n_{\mathrm{critic}}\) RMSProp critic steps per generator step; no log-sigmoid GAN
  loss; defaults \(\alpha=5\cdot10^{-5}\), \(c=0.01\), \(n_{\mathrm{critic}}=5\).

## Related

- applies [[wasserstein-distance]] — trains generative models by (approximately) minimizing \(W_1\)
- applies [[monge-kantorovich-formulations]] — uses the Kantorovich–Rubinstein dual of \(W_1\)
- background-for [[neural-optimal-transport]] — the cost-only adversarial baseline that later neural OT map/plan solvers go beyond
- background-for [[2023-korotin-neural-optimal-transport]] — Korotin contrasts WGAN-style cost estimation with learning stochastic OT maps
- benchmarks [[2019-yang-scalable-unbalanced-ot-gans]] — sibling adversarial transport learner; Yang et al. recover a map (+ mass scale) rather than only \(W\)
- [[Sources MOC]]
- [[Optimal Transport MOC]]
