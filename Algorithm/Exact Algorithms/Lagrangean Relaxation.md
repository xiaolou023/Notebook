# Linear Programming Duality

Given the primal problem

$$
\begin{aligned} 
\text { min. } & \mathbf{c}^{\prime} \mathbf{x} \\ \text { s.t. } & \mathbf{A x} \geq \mathbf{b} \\
 & \mathbf{D x} \geq \mathbf{d} 
\end{aligned}
$$

Let $P = \{\mathbf{x} | \mathbf{D x} \geq \mathbf{d}\}$, we define the *dual problem* as

$$
\begin{aligned}
\text { maximize } & g(\mathbf{p}) \\
\text { subject to } & \mathbf{p} \geq \mathbf{0} 
\end{aligned}
$$
where 
$$
g(\mathbf{p})= \text{min}_{\mathbf{x} \in P}[\mathbf{c}^{\prime} \mathbf{x}+\mathbf{p}^{\prime}(\mathbf{b}-\mathbf{A} \mathbf{x})]
$$



**weak duality**

if $\mathbf{x^\star}$ is primal feasible, and $\mathbf{p^\star}$ is dual feasible, then

$$
g(\mathbf{p^\star}) \leq \mathbf{c}^{\prime} \mathbf{x^\star}
$$

**Strong duality**

If $\mathbf{x^\star}$ is primal optimal solution, and $\mathbf{p^\star}$ is dual optimal solution, then

$$
g(\mathbf{p^\star}) = \mathbf{c}^{\prime} \mathbf{x^\star}
$$

# Integer Programming Duality

Given the primal problem

$$
\begin{aligned} 
\text { min. } & \mathbf{c}^{\prime} \mathbf{x} \\ \text { s.t. } & \mathbf{A x} \geq \mathbf{b} \\
 & \mathbf{D x} \geq \mathbf{d} \\
 & \mathbf{x} \text{ integer}
\end{aligned}
$$

Let $X = \{\mathbf{x} \text{ integer} | \mathbf{D x} \geq \mathbf{d}\}$, where $\mathbf{D x} \geq \mathbf{d}$ are relatively nice constraints in primal problem, we define the *Lagrangean dual* as

$$
\begin{aligned}
\text { maximize } & Z(\mathbf{p}) \\
\text { subject to } & \mathbf{p} \geq \mathbf{0} 
\end{aligned}
$$
where 
$$
Z(\mathbf{p})= \text{min}_{\mathbf{x} \in X}[\mathbf{c}^{\prime} \mathbf{x}+\mathbf{p}^{\prime}(\mathbf{b}-\mathbf{A} \mathbf{x})]
$$

**Quaility of Bounds**

Let $Z_D$ be optimal cost to *Lagrangean dual*, $Z_{IP}$ be optimal cost to primal integer problem, $Z_{LP}$ be optimal cost to linear relaxation to primal problem.

1. In general, we have
   $$
   Z_{LP} \leq Z_D \leq Z_{IP}
   $$
2. $Z_D$ is equal to the optimal cost of the following linear programming problem:
   $$
   \begin{aligned}
    \text { min. } & \mathbf{c}^{\prime} \mathbf{x} \\
    \text { s.t. } & \mathbf{A x} \geq \mathbf{b} \\
    & \mathbf{x} \in Conv(X)   
   \end{aligned}
   $$
   where $Conv(X)$ is the convex hull of X.
3. We have $Z_{IP} = Z_{D}$ for all cost vectors $\mathbf{c}$, if and only if 
   $$
   \text { CH }(X \cap\{\mathbf{x} | \text { Ax } \geq \mathbf{b}\})=\operatorname{CH}(X) \cap\{\mathbf{x} | \mathbf{A} \mathbf{x} \geq \mathbf{b}\} 
   $$
4. We have $Z_{LP} = Z_{D}$ for all cost vectors $\mathbf{c}$, if 
   $$
   \operatorname{CH}(X)=\{\mathbf{x} | \mathbf{D} \mathbf{x} \geq \mathbf{d}\}
   $$