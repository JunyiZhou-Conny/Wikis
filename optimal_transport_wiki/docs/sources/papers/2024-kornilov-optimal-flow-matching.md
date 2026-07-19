---
title: "Optimal Flow Matching: Learning Straight Trajectories in Just One Step"
type: source
status: done
date: 2026-07-19
source_kind: paper
tier: A
venue: "NeurIPS 2024"
year: 2024
authors: ["Kornilov", "Mokrov", "Gasnikov", "Korotin"]
approx_citations: 20
doi: "10.48550/arXiv.2403.13117"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/neural-ot
  - topic/wasserstein
  - method/neural-ot
  - method/icnn
---

# Optimal Flow Matching: Learning Straight Trajectories in Just One Step

Kornilov, Mokrov, Gasnikov & Korotin, *NeurIPS 2024*. **Optimal Flow Matching (OFM)** —
recover the straight quadratic OT displacement in a *single* flow-matching step by restricting
the FM vector field to gradients of convex (ICNN) potentials.

## Summary

Flow Matching (FM) and its straightening variants (Rectified Flow, OT-CFM / minibatch OT) aim
for near-linear trajectories so inference needs few ODE steps, but RF accumulates iteration error
and OT-CFM only approximates dynamic OT via biased mini-batch plans. OFM instead minimizes the
FM loss **only over "optimal" vector fields** — those whose paths are linear by design and of the
form \(z_t=(1-t)z_0+t\nabla\Psi(z_0)\) for a convex Brenier potential \(\Psi\). Theorem 1 shows that,
for *any* initial plan \(\pi\in\Pi(p_0,p_1)\), minimizing the OFM loss over convex \(\Psi\) is
equivalent to minimizing the dual \(W_2\) OT loss — so one FM iteration recovers the Benamou–Brenier
quadratic OT flow. At inference the map is \(T=\nabla\Psi\) (no ODE solve). Code:
https://github.com/Jhomanik/Optimal-Flow-Matching.

## Key claims / results

- **Optimal vector fields:** \(u^\Psi\) generates straight paths with \(z_1=\nabla\Psi(z_0)\); the
  dynamic-\(W_2\) solution lies in this class (Brenier).
- **Thm. 1:** \(\arg\min_{\text{convex }\Psi}\mathcal{L}_{\mathrm{OFM}}^\pi(\Psi)=\arg\min_{\text{convex }\Psi}\mathcal{L}_{\mathrm{OT}}(\Psi)\)
  for every \(\pi\in\Pi(p_0,p_1)\) — initial plan choice is theoretically justified, not a heuristic.
- **Tractable OT distance (Prop. 4):** for optimal fields, \(\mathrm{dist}(u^\Psi,u^*)\) equals the
  OFM loss up to a \(\Psi\)-independent constant, so OFM descent closes the gap to the dynamic OT field.
- **Practice:** parametrize \(\Psi\) with ICNNs; invert the flow map at each \(x_t\) by a strongly convex
  subproblem (Eq. 17); closed-form OFM gradient via Hessian of \(\Psi\) (Prop. 1).
- **Benchmarks:** on the continuous \(W_2\) UVP suite (Korotin et al.), OFM (esp. minibatch init)
  beats OT-CFM / RF / \(c\)-RF among FM methods through \(D=256\); 2D Gaussian→8-Gaussians maps
  match across independent / minibatch / antiminibatch \(\pi\); ALAE latent Adult→Child FID
  competitive with \(c\)-RF and better than OT-CFM.
- **Limits:** quadratic cost only; ICNN capacity/scalability; MLP substitution failed to converge.

## Methodology

- Restrict FM (Eq. 10) to \(u=u^\Psi\) for convex \(\Psi_\theta\) (ICNN); sample \((x_0,x_1)\sim\pi\),
  \(t\sim U[0,1]\), \(x_t=(1-t)x_0+tx_1\).
- Recover \(z_0=(\phi_t^\Psi)^{-1}(x_t)\) by convex minimization; evaluate Monte-Carlo OFM loss /
  gradient (Alg. 1); optional \(\pi=\) independent or mini-batch OT.
- Inference: push \(x_0\mapsto\nabla\Psi_\theta(x_0)\) (or evaluate the closed-form straight path) —
  simulation-free transport.

## Related

- applies [[neural-optimal-transport]] — ICNN Brenier potential + FM yields a neural OT map/flow in one step
- applies [[monge-kantorovich-formulations]] — dual convex \(\Psi\) / Brenier map \(T=\nabla\Psi\); Kantorovich plans \(\pi\) as FM conditions
- applies [[wasserstein-distance]] — recovers quadratic \(W_2\) / Benamou–Brenier dynamic OT
- extends [[2023-korotin-neural-optimal-transport]] — same lead lab / neural OT line; OFM bridges dual OT to flow matching instead of maximin weak-OT maps
- benchmarks [[2023-bunne-cellot-neural-ot]] — both use ICNN potentials for Monge maps; OFM via FM loss, CellOT via maximin dual for single-cell perturbations
- contradicts [[2024-tong-ot-cfm-minibatch]] — argues mini-batch OT-CFM is a biased heuristic; OFM makes any \(\pi\) exact for quadratic OT (draft sibling)
- extends [[2023-pooladian-multisample-flow-matching]] — same FM+coupling agenda; OFM restricts the field class rather than refining the coupling (draft sibling)
- applies [[2000-benamou-dynamic-formulation]] — OFM's target is the Benamou–Brenier quadratic flow (draft sibling)
- [[Sources MOC]]
- [[Optimal Transport MOC]]
