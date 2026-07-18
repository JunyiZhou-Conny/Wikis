---
title: "Learning with a Wasserstein Loss"
type: source
status: done
date: 2026-07-18
source_kind: paper
tier: A
venue: "NeurIPS 2015"
year: 2015
authors: ["Frogner", "Zhang", "Mobahi", "Araya-Polo", "Poggio"]
approx_citations: 800
doi: "10.48550/arXiv.1506.05439"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/wasserstein
  - topic/supervised-ot
  - method/sinkhorn
  - method/entropic-ot
---

# Learning with a Wasserstein Loss

Frogner, Zhang, Mobahi, Araya-Polo & Poggio, *NeurIPS 2015*. The canonical early use of
**Wasserstein distance as a supervised multi-label loss** — Sinkhorn-smoothed OT that respects
a ground metric on the label space.

## Summary

When outputs are non-negative measures over a finite set with a known **ground metric**
(semantic similarity among classes/tags), standard KL / logistic losses treat coordinates
independently and ignore that structure. This paper defines an ERM loss as the **Wasserstein
distance** between predicted and target measures, so misplacing mass onto a near-equivalent label
costs less than onto a distant one. Exact OT is too expensive for gradient descent; they use
Cuturi's **entropic regularization** and Sinkhorn scaling to get a differentiable surrogate, and
propose a novel **relaxed transport** objective with soft KL marginal penalties that extends the
loss to **unnormalized** measures. A Rademacher generalization bound justifies the ERM, and
experiments on synthetic label noise and Yahoo/Flickr tag prediction show metric-aware
predictions that beat a divergence baseline.

## Key claims / results

- First (to their knowledge) use of Wasserstein distance as a **discriminative / supervised**
  loss, not only for retrieval, barycenters, or unsupervised alignment.
- Entropic OT yields a practical Sinkhorn iteration for \(\partial W/\partial h(x)\); the dual
  scaling vector \(u\) gives the gradient on the simplex.
- **Relaxed transport** replaces hard marginal equalities with KL penalties — an early soft-marginal
  / unbalanced-style formulation that still admits Sinkhorn-like fixed-point updates.
- Statistical learning: for \(p=1\), expected \(W_1\) of the ERM approaches the best-in-class risk
  (Rademacher bound); in multiclass, the same ERM controls expected **semantic** distance of the
  argmax prediction, not only 0–1 error.
- Empirically: on MNIST with a digit-line metric, larger \(p\) spreads posterior mass onto
  neighboring digits; on Flickr tag prediction with word2vec tag distances, top-\(K\) transport
  cost beats a KL/divergence baseline, especially when tags are redundant.

## Methodology

- Discrete Kantorovich \(W_p^p\) between prediction \(h(x)\) and label \(y\) with cost matrix
  \(M_{\kappa,\kappa'}=d_{\mathcal{K}}^p(\kappa,\kappa')\).
- Entropic surrogate \(\inf_{T\in\Pi(h,y)}\langle T,M\rangle-\lambda^{-1}H(T)\); \(T^\*=\mathrm{diag}(u)K\mathrm{diag}(v)\),
  \(K=\exp(-\lambda M)\); Sinkhorn for \(u,v\); gradient \(\alpha=\log u-\log(u^\top\mathbf{1}_K/K)\).
- Unnormalized case: minimize \(\langle T,M\rangle-\lambda^{-1}H(T)+a\,\mathrm{KL}(T\mathbf{1}\|h)+b\,\mathrm{KL}(T^\top\mathbf{1}\|y)\);
  soft-marginal Sinkhorn updates; \(\nabla_h W=a(1-T\mathbf{1}\oslash h)\).
- Train by SGD on the empirical Wasserstein risk (softmax → simplex for the normalized case).

## Related

- introduces [[wasserstein-loss]] — Wasserstein / entropic OT as a supervised multi-label ERM loss
- applies [[wasserstein-distance]] — the loss is \(W_p\) between predicted and target label measures
- applies [[entropic-regularization-sinkhorn]] — Sinkhorn supplies the scalable, differentiable surrogate
- applies [[monge-kantorovich-formulations]] — discrete Kantorovich plans over the label simplex
- background-for [[balanced-vs-unbalanced-ot]] — relaxed KL-marginal transport anticipates soft-marginal unbalanced OT
- extends [[2013-cuturi-sinkhorn-distances]] — turns Cuturi's Sinkhorn distance into a supervised learning loss
- background-for [[2019-sejourne-unbalanced-sinkhorn-divergences]] — earlier soft-marginal entropic transport; Séjourné later debiases unbalanced Sinkhorn losses
- [[Sources MOC]]
- [[Optimal Transport MOC]]
