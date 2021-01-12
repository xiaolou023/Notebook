# Benders decomposition for asymmetric traveling salesman problem

## Asymmetric travelling salesman problem

ATSP instance is defined on a directed graph $G = (V, A)$:

- $V = \{0, \ldots, n - 1\}$, $V_0 = V \setminus \{0\}$; set of nodes
- $A = \{(i,j): i \in V, j \in V, i \neq j\}$; set of arcs
- $\delta^+(i) = \{(i,j) \in A: j \in V\}$, $\forall i \in V$
- $\delta^-(i) = \{(j,i) \in A: j \in V\}$, $\forall i \in V$
- $c_{i,j}$ = traveling cost associated with $(i,j) \in A$

### Flow-based MILP model

- $x_{ij}$ = 1, if arc $(i,j)$ is selected; $x_{ij} = 0$, otherwise. ($\forall (i,j) \in A$)
- $y_{ijk} = $ flow of commodity $k$ through arc $(i,j)$. ($\forall k \in V_0, \forall (i,j) \in A$)

$$
\begin{align}
% objective
\min \quad & \sum_{(i,j) \in A} c_{ij} \cdot x_{ij} \\
% degree constraints
& \sum_{(i,j) \in \delta^+_i} x_{ij} = 1 & \quad \forall i \in V \\
& \sum_{(j,i) \in \delta^-_i} x_{ji} = 1 & \quad \forall i \in V \\
% binary constraints on arc variables
& x_{ij} \in \{0, 1\} & \forall (i,j) \in A \\
% flow constraints
& \sum_{(i,j) \in \delta^+_i} y_{ijk} - \sum_{(j,i) \in \delta^-_i} y_{jik} = q_{ik} & \forall k\in V_0, \forall i \in V \\
% capacity constraints
& y_{ijk} \leq x_{ij} & \forall k \in V_0, \forall (i,j) \in A \\
% nonegativity of flow variables
& y_{ijk} \geq 0 & \forall k \in V_0, \forall (i,j) \in A
\end{align}
$$

where $q_{ik} = 1$, if $i = 0$; $q_{ik} = -1$, if $i ==k$; $q_{ik} = 0$, otherwise.

### Master ILP

- $x_{ij}$ = 1, if arc $(i,j)$ is selected; $x_{ij} = 0$, otherwise. ($\forall (i,j) \in A$)

objective (1) together with constraints (2) - (4)

### Worker LP

#### Primal subproblem

To search a feasible solution subject to constraints (5)-(8), when $x_{ij}$ is fixed to $\bar{x}_{ij}$.

#### Dual subproblem

Let $u_{ik}$, $\hat{v}_{ijk}$ be dual variables associated with constraints (5)(6), respectively. $u_{ij} \in \R, \hat{v}_{ijk} \leq 0$.

Let $v_{ijk} = - \hat{v}_{ijk} \Rightarrow \hat{v}_{ijk} = - v_{ijk}$.
$$
\begin{align}
% max -f(x) => min f(x)
\min \quad & \sum_{k \in V_0} \sum_{(i,j) \in A} v_{ijk}\bar{x}_{ij} - \sum_{k \in V_0} u_{0k} + \sum_{k \in V_0}u_{kk} \\
s.t \quad & u_{ik} - u_{jk} \leq v_{ijk} \quad \forall (i,j) \in A, \forall k \in V_0 \\
& v_{ijk} \geq 0 \\
\end{align}
$$

### Benders Cuts

If the dual subproblem turns out unbounded, the primal subproblem is infeasible. The cut is

$\sum_{(i,j) \in A}\sum_{k \in V_0} v_{ijk}x_{ij} \geq \sum_{k \in V_0} u_{0k} - \sum_{k \in V_0} u_{kk}$








