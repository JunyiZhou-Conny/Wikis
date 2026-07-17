---
title: "Multisample Flow Matching: Straightening Flows with Minibatch Couplings"
type: source
status: done
date: 2026-07-17
source_kind: paper
tier: A
venue: "ICML 2023"
year: 2023
authors: ["Pooladian", "Ben-Hamu", "Domingo-Enrich", "Amos", "Lipman", "Chen"]
approx_citations: 300
doi: "10.48550/arXiv.2304.14772"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/neural-ot
  - topic/wasserstein
  - method/neural-ot
---

# Multisample Flow Matching: Straightening Flows with Minibatch Couplings

Pooladian, Ben-Hamu, Domingo-Enrich, Amos, Lipman & Chen, *ICML 2023* (Meta FAIR).
Generalizes Flow Matching to **non-independent minibatch OT couplings** so CNF paths stay
marginally correct while becoming straighter and cheaper to simulate.

## Summary

Standard Flow Matching / CondOT builds conditional paths between *independently* sampled noise
and data, so the learned marginal flow need not be close to dynamic OT and still has nonzero
gradient variance at optimum. **Multisample Flow Matching** samples \(k\)-sets from each
marginal, builds a doubly-stochastic coupling \(\pi\) on the batch (BatchOT, BatchEOT, or
cheaper stable/heuristic permutations), then trains Joint CFM on pairs drawn from \(\pi\).
Because \(\pi\) is doubly stochastic, the induced joint keeps the correct population marginals
(Lemma 4.1) — unlike static maps fit to minibatch OT, which collapse to barycentric projections.
As \(k\to\infty\), BatchOT drives Joint-CFM loss, path curvature, and transport cost toward the
\(W_2\) optimum (Thm. 4.2), yielding a simulation-free route to approximate OT maps.

## Key claims / results

- **Joint CFM** (Eq. 15) is valid for *any* coupling with the right marginals; independent CondOT
  is the uniform special case \(\pi(i,j)=1/k\).
- Gradient-variance proxy at fixed \((t,x)\) is bounded by the Joint-CFM objective (Lemma 3.2), so
  better couplings speed training.
- **BatchOT** (exact minibatch \(W_2\) via Hungarian / network simplex) and **BatchEOT** (Sinkhorn)
  produce straighter flows; Stable / Heuristic Gale–Shapley variants are cheaper \(O(k^2)\)
  surrogates that often match BatchOT empirically.
- On ImageNet \(32\times32\) / \(64\times64\): 30–60% fewer NFEs to hit a fixed FID vs CondOT FM,
  with only ~1–4% training-time overhead; better sample consistency across NFE budgets; no
  degradation in FID / BPD at full simulation.
- When only an oracle minibatch coupling (unknown cost) is available, the dynamic Joint-CFM map
  matches the target marginal and is no worse in cost than the batch OT plan — static regressors
  fail to preserve the marginal (Table 4).

## Methodology

- Draw mini-batches \(\{x_0^{(i)}\},\{x_1^{(i)}\}\); compute coupling \(\pi\) (POT exact OT,
  Sinkhorn, or stable matching); sample pairs \((x_0,x_1)\sim\pi\); regress \(v_\theta(t,x_t)\) onto
  the CondOT field \(u_t=x_1-x_0\) along \(x_t=(1-t)x_0+tx_1\).
- Training stays simulation-free (no ODE integrate-through); inference integrates the learned
  vector field with Euler or adaptive ODE solvers.
- Ablations contrast CondOT vs Stable / Heuristic / BatchEOT / BatchOT on 2D checkerboards and
  downsampled ImageNet; also probe unknown-cost oracle couplings in 2–64D.

## Related

- applies [[neural-optimal-transport]] — learns continuous transport as a CNF vector field conditioned on minibatch OT plans
- applies [[monge-kantorovich-formulations]] — BatchOT / BatchEOT are discrete Kantorovich couplings used as FM training joints
- applies [[wasserstein-distance]] — squared-Euclidean BatchOT; asymptotic near-\(W_2\) transport cost of the learned flow
- applies [[entropic-regularization-sinkhorn]] — BatchEOT replaces exact batch OT with Sinkhorn doubly-stochastic plans
- extends [[2023-korotin-neural-optimal-transport]] — sibling neural OT; simulation-free FM + minibatch couplings vs maximin dual for strong/weak costs
- applies [[2013-cuturi-sinkhorn-distances]] — computational engine behind BatchEOT minibatch plans
- benchmarks [[2023-bunne-cellot-neural-ot]] — both recover transport maps; Pooladian via CNF + BatchOT, CellOT via ICNN Monge maps
- [[Sources MOC]]
- [[Optimal Transport MOC]]
