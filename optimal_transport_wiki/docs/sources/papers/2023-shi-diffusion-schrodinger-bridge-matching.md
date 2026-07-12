---
title: "Diffusion Schrödinger Bridge Matching"
type: source
status: done
date: 2026-07-12
source_kind: paper
tier: A
venue: "NeurIPS 2023"
year: 2023
authors: ["Shi", "De Bortoli", "Campbell", "Doucet"]
approx_citations: 200
doi: "10.48550/arXiv.2303.16852"
source_path: ""
tags:
  - source
  - domain/ml
  - domain/literature
  - topic/neural-ot
  - topic/wasserstein
  - method/entropic-ot
  - method/neural-ot
---

# Diffusion Schrödinger Bridge Matching

Shi, De Bortoli, Campbell & Doucet, *NeurIPS 2023*. A frontier **dynamic entropic-OT** solver:
Schrödinger bridges via Iterative Markovian Fitting + bridge-matching regression — the diffusion-side
counterpart to static Sinkhorn and neural Monge maps.

## Summary

Denoising diffusion and flow matching transport mass between distributions, but their paths are
not guaranteed to be close to (dynamic) optimal transport. Schrödinger bridges (SBs) are the
**dynamic entropy-regularized OT** problem: among path measures with fixed endpoint marginals,
pick the one closest in KL to a reference diffusion (equivalently, a mixture of reference bridges
weighted by a static entropic coupling). Prior diffusion SB solvers based on Iterative Proportional
Fitting (IPF) accumulate discretization and “forgetting” errors. This paper introduces **Iterative
Markovian Fitting (IMF)** — alternating projections onto Markov path measures and the reciprocal
class of the reference — and **Diffusion Schrödinger Bridge Matching (DSBM)**, which implements
each Markovian projection as a bridge-matching regression. IMF always preserves the endpoint
marginals; DSBM recovers Bridge/Flow Matching and Rectified Flow as special/limiting cases and
outperforms prior DSB numerics on transfer tasks.

## Key claims / results

- The SB is the unique path measure that is **Markov**, in the **reciprocal class** of the reference
  \(Q\), and has the prescribed endpoint marginals \(\pi_0,\pi_T\) (Prop. 5).
- **IMF** alternates \(\mathrm{proj}_{\mathcal{M}}\) and \(\mathrm{proj}_{\mathcal{R}(Q)}\); unlike IPF, every iterate keeps
  \(P_0=\pi_0\) and \(P_T=\pi_T\). Fixed points of IMF are the SB (Prop. 7).
- **DSBM** learns forward/backward drifts by MSE regression on Doob \(h\)-transform targets from
  sampled bridges; alternating forward and backward Markovian projections prevents terminal-marginal
  bias accumulation (Prop. 8, Alg. 1).
- **DSBM-IPF** (init from the reference forward coupling) recovers classical IPF/DSB iterates in
  theory but trains continuously in time and re-projects onto the reciprocal class; **DSBM-IMF**
  (init \(\pi_0\otimes\pi_T\)) is the Rectified-Flow analogue with \(\sigma>0\).
- Empirically: lower path energy / better \(\mathbb{W}_2\) than DSB, FM, CFM on 2D transports; accurate
  high-d Gaussian SB moments where DSB/RF degrade; stable MNIST↔EMNIST and CelebA attribute
  transfer without the FID collapse seen in DSB/RF; ~30% faster runtime than DSB on the digit
  transfer. Limitation: gains vs generative baselines are clearer on *general* transport than on
  pure noise→data generation.

## Methodology

- Static SB / EOT: \(\Pi_{0,T}^{\mathrm{SB}}=\arg\min\{\mathrm{KL}(\Pi_{0,T}\|Q_{0,T}):\Pi_0=\pi_0,\Pi_T=\pi_T\}\);
  for Brownian reference this is entropic OT with cost \(\|x_0-x_T\|^2\).
- Dynamic SB: \(\argmin_P\{\mathrm{KL}(P\|Q):P_0=\pi_0,P_T=\pi_T\}\), realized as
  \(\Pi_{0,T}^{\mathrm{SB}}Q|_{0,T}\).
- Markovian projection of a bridge mixture \(\Pi=\Pi_{0,T}Q|_{0,T}\) yields an SDE whose drift is the
  conditional expectation of the bridge Doob drift (learned by regression).
- Reciprocal projection rebuilds \(\Pi\leftarrow M_{0,T}Q|_{0,T}\) from cached endpoint pairs of the
  current Markov process — no full-trajectory score matching per IPF step.

## Related

- introduces [[schrodinger-bridge]] — IMF/DSBM as a practical dynamic EOT solver
- extends [[entropic-regularization-sinkhorn]] — lifts static Sinkhorn/EOT to a diffusion path measure
- applies [[neural-optimal-transport]] — neural drifts for continuous transport, via bridges rather than dual potentials
- background-for [[wasserstein-distance]] — \(\sigma\to 0\) recovers dynamic OT / Benamou–Brenier; experiments report \(\mathbb{W}_2\)
- extends [[2013-cuturi-sinkhorn-distances]] — continuous-time reciprocal of discrete entropic OT / Sinkhorn–IPF
- benchmarks [[2023-korotin-neural-optimal-transport]] — sibling neural transport learner; DSBM targets dynamic EOT paths vs Korotin’s static strong/weak plans
- [[Sources MOC]]
- [[Optimal Transport MOC]]
