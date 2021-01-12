# Lagrangian relaxation for RCPSP (with additional constraints)

## Approach 1

Problems: RCPSP[^1], RCPSP with generalized precedence relations[^2]; RCPSP with net present value; ...

Original model: time-indexed formulation

Lagrangian relaxation: **relaxing the resource constraints**

> Each resource constraint is linked with a Lagrangian multiplier $\lambda_{kt}$.
>
> The Lagrangian multiplier $\lambda_{kt}$ can be interpreted as the unit-price for using resource $k$ at time period $t$.

Lagrangian problem: $LR(\lambda)$

> Each Lagrangian problem is a special case of the scheduling problem with start-time-dependent costs.[^1] 
>
> The scheduling problem with with start-time-dependent costs is transformed into minimal cut problem.[^1] 

The solution to Lagrangian problem:

- **minimum cut problem (max-flow algorithm)**
- Mathematical solver

Lagrangian dual problem: $\max_{\lambda} LR(\lambda)$

The solution to Lagrangian dual problem: 

- **sub-gradient algorithm**[^3][^4]

## Approach 2

original problem

Lagrangian relaxation

Lagrangian problem: the Lagrangian problem could be decomposed into some independent subproblems

> To decompose original problem into independent subproblems, usually the variable linking constraints are relaxed.

## References

[^1]: Möhring, R. H., Schulz, A. S., Stork, F., & Uetz, M. (2003). Solving Project Scheduling Problems by Minimum Cut Computations. *Management Science*, *49*(3), 330–350. https://doi.org/10.1287/mnsc.49.3.330.12737
[^2]:Schwindt, C., & Zimmermann, J. (Eds.). (2015). Handbook on Project Management and Scheduling Vol.1. Springer International Publishing. https://doi.org/10.1007/978-3-319-05443-8
[^3]:Bertsimas, D., & Tsitsiklis, J. N. (1997). Introduction to linear optimization. Athena Scientific.
[^4]:Ayala, M., Artigues, C., & Gacias, B. (2010). Lagrangian relaxation-based lower bound for resource-constrained modulo scheduling. Electronic Notes in Discrete Mathematics, 36, 191–198. https://doi.org/10.1016/j.endm.2010.05.025








