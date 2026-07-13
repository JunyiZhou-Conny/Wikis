---
title: "A computational fluid mechanics solution to the Monge-Kantorovich mass transfer problem"
type: source
status: done
date: 2026-07-13
source_kind: paper
tier: A
venue: "Numerische Mathematik"
year: 2000
authors: ["Benamou", "Brenier"]
approx_citations: 1650
doi: "10.1007/s002110050002"
source_path: ""
tags:
  - source
  - domain/math
  - domain/literature
  - topic/wasserstein
  - topic/dynamic-ot
  - method/benamou-brenier
---

# A computational fluid mechanics solution to the Monge-Kantorovich mass transfer problem

Benamou & Brenier, *Numerische Mathematik* 2000. The canonical **dynamic** formulation of
quadratic optimal transport — reset the Monge–Kantorovich problem as a continuum-mechanics
least-action principle and solve it with an augmented Lagrangian.

## Summary

Rather than attacking the Monge–Ampère equation for the convex potential of the optimal map, this
paper rewrites the squared $L^2$ Kantorovich (Wasserstein) distance as an infimum of kinetic
energy over space–time densities and velocities obeying the continuity equation between fixed
endpoints $\rho_0$ and $\rho_T$. The resulting convex space–time problem in $(\rho,m=\rho v)$ has
*linear* constraints, yields a natural geodesic interpolant, and is solved by an ALG2 augmented
Lagrangian / Uzawa scheme whose steps are a constant-coefficient Laplace solve, a pointwise dual
projection, and a trivial density–momentum update.

## Key claims / results

- **Dynamic characterization:** $W_2^2(\rho_0,\rho_T)$ equals
  $\inf T\int_0^T\int \rho|v|^2\,dx\,dt$ over $(\rho,v)$ with $\partial_t\rho+\nabla\cdot(\rho v)=0$,
  $\rho(0)=\rho_0$, $\rho(T)=\rho_T$ (Proposition 1.1).
- Optimality conditions are a **pressureless potential flow**: $v=\nabla\phi$ with Hamilton–Jacobi
  $\partial_t\phi+\tfrac12|\nabla\phi|^2=0$.
- Reintroducing time trades a nonconvex Monge map constraint for a **convex** minimization in
  $(\rho,m)$ with linear continuity constraints — computationally preferable despite the extra
  dimension.
- The ALG2 scheme reduces each Uzawa iteration to (i) a space–time Neumann Laplace solve for
  $\phi$, (ii) pointwise convex projection of dual variables $(a,b)$, (iii) updating $(\rho,m)$;
  demonstrated in 2-D periodic examples including topology-changing Gaussian-array transfers.

## Methodology

- Continuity-constrained kinetic-energy action; Legendre transform of $\tfrac12\rho|v|^2$ introduces
  dual fields $(a,b)$; augment the Lagrangian with $\|a-\partial_t\phi\|^2+\|b-\nabla\phi\|^2$ and
  apply Fortin–Glowinski ALG2 / Uzawa.

## Related

- introduces [[benamou-brenier-formulation]] — the dynamic / fluid-mechanics characterization of $W_2$
- applies [[monge-kantorovich-formulations]] — reformulates the $L^2$ Monge–Kantorovich problem without solving Monge–Ampère directly
- applies [[wasserstein-distance]] — equates $W_2^2$ to a space–time kinetic-energy infimum
- background-for [[wasserstein-fisher-rao-metric]] — WFR’s dynamic geodesics extend this continuity-equation action with a growth term
- background-for [[2018-chizat-unbalanced-ot-formulations]] — unbalanced dynamic formulations build on this Benamou–Brenier template
- background-for [[2019-peyre-computational-optimal-transport]] — monograph later surveys dynamic OT rooted here
- [[Sources MOC]]
- [[Optimal Transport MOC]]
