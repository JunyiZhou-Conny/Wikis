---
title: Monge and Kantorovich formulations of OT
type: concept
status: done
date: 2026-07-07
tags:
  - concept
  - domain/math
  - topic/optimal-transport
distilled_from:
  - "[[2013-cuturi-sinkhorn-distances]]"
  - "[[2023-bunne-cellot-neural-ot]]"
  - "[[2018-alvarez-melis-gromov-wasserstein-alignment]]"
  - "[[2019-peyre-computational-optimal-transport]]"
  - "[[2023-korotin-neural-optimal-transport]]"
  - "[[2000-benamou-dynamic-formulation]]"
---

# Monge and Kantorovich formulations of OT

The two classical ways to pose optimal transport: **Monge** seeks a deterministic map T pushing
one measure onto another at minimal cost; **Kantorovich** relaxes this to a **coupling** (joint
distribution) γ, giving a linear program with a well-behaved dual.

## Why it matters / where it shows up

Almost every OT method is "which formulation, solved how": Kantorovich's coupling underlies
discrete/entropic solvers; the **dual** underlies neural-OT (learn potentials, recover the Monge
map as their gradient). Knowing the primal/dual pair explains why methods look so different.

## Details

- **Monge (1781):** minimize E‖X − T(X)‖² over maps with T#μ = ν. Non-convex; a map may not exist.
- **Kantorovich (1942):** minimize ⟨γ, C⟩ over couplings γ ∈ Π(μ, ν) with the given marginals — a
  linear program, always solvable ([[2013-cuturi-sinkhorn-distances]], [[2018-alvarez-melis-gromov-wasserstein-alignment]]).
- **Duality:** the dual is a concave problem over potentials (f, g); Brenier/Knott–Smith link the
  optimal map to ∇f*, which **neural OT** exploits ([[2023-bunne-cellot-neural-ot]]). Weak OT
  extends the dual via a \(C\)-transform over conditional measures, enabling stochastic plans
  ([[2023-korotin-neural-optimal-transport]]).
- The monograph [[2019-peyre-computational-optimal-transport]] is the reference treatment.
- **Dynamic reformulation:** Benamou–Brenier rewrite the $L^2$ problem as a continuity-constrained
  kinetic-energy action, avoiding direct Monge–Ampère solves ([[2000-benamou-dynamic-formulation]],
  [[benamou-brenier-formulation]]).

## Related

- introduces [[2013-cuturi-sinkhorn-distances]] — regularizes the Kantorovich primal
- applies [[2023-bunne-cellot-neural-ot]] — parameterizes the dual potentials to recover a Monge map
- applies [[2023-korotin-neural-optimal-transport]] — maximin dual for strong/weak costs → stochastic maps
- background-for [[2018-alvarez-melis-gromov-wasserstein-alignment]] — GW builds on the coupling polytope
- extends [[balanced-vs-unbalanced-ot]] — unbalanced OT relaxes the Kantorovich marginal constraints
- applies [[2000-benamou-dynamic-formulation]] — fluid-mechanics path to the same $L^2$ Monge–Kantorovich problem
- extends [[benamou-brenier-formulation]] — dynamic continuity-equation equivalent of the static formulations
