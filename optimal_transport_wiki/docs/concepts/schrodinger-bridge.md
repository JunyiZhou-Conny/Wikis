---
title: Schrödinger bridge (dynamic entropic OT)
type: concept
status: done
date: 2026-07-12
tags:
  - concept
  - domain/ml
  - domain/math
  - topic/wasserstein
  - topic/neural-ot
  - method/entropic-ot
distilled_from:
  - "[[2023-shi-diffusion-schrodinger-bridge-matching]]"
  - "[[2013-cuturi-sinkhorn-distances]]"
  - "[[2019-peyre-computational-optimal-transport]]"
---

# Schrödinger bridge (dynamic entropic OT)

The **Schrödinger bridge (SB)** is the path measure with fixed endpoint marginals that stays
closest in KL to a reference diffusion — equivalently, a **dynamic** formulation of
**entropy-regularized optimal transport**.

## Why it matters / where it shows up

Static Sinkhorn gives a coupling; generative modeling needs a *process* that carries samples from
one distribution to another. SBs supply that process with OT-like geometry (minimal kinetic energy
under entropic smoothing), connecting discrete EOT to diffusion / flow-matching methods.

## Details

- For a Brownian reference, the static SB coupling is entropic OT with quadratic cost — the same
  object Sinkhorn computes on discrete supports ([[2013-cuturi-sinkhorn-distances]],
  [[2019-peyre-computational-optimal-transport]]).
- Dynamically, the SB is the unique measure that is Markov, shares the reference’s bridges
  (reciprocal class), and matches the prescribed endpoints.
- **IMF + DSBM** ([[2023-shi-diffusion-schrodinger-bridge-matching]]) compute it by alternating
  Markovian and reciprocal projections, learning drifts with bridge-matching regression — an
  alternative to IPF-style Diffusion Schrödinger Bridge solvers.
- As the diffusion coefficient \(\sigma\to 0\), the SB collapses toward dynamic (Benamou–Brenier) OT;
  flow matching / rectified flow appear as deterministic limits.

## Related

- introduces [[2023-shi-diffusion-schrodinger-bridge-matching]] — IMF/DSBM numerical solver
- extends [[2013-cuturi-sinkhorn-distances]] — discrete entropic OT is the static SB coupling
- background-for [[2019-peyre-computational-optimal-transport]] — EOT / dynamic OT reference treatment
- contrasts [[neural-optimal-transport]] — dual/map neural OT vs path-measure SB solvers
- extends [[entropic-regularization-sinkhorn]] — same entropy bias, now on path space
