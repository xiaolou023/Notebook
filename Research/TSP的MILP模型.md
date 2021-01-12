# Traveling Salesman Problem (TSP)

## Model 1

$x_{ij}$ = 1 if and only if the vehicle traverses the arc $(i, j)$.

$u_i$ integer variables
$$
\begin{aligned}
\text{min} \quad & \sum_{i = 1}^{n}\sum_{j = 1}^n d_{ij}x_{ij} & \quad \\
\text{s.t.} \quad & \sum_{j = 1}^n x_{ij} = 1 & \forall i \in V \\
& \sum_{x = 1}^n x_{ij} = 1 & \forall j \in V \\
% subtour elimination
& u_i - u_j + (n - 1)x_{ij} \leq n - 2 & \forall i,j \in V \setminus \{0\} \\
& x_{ij} \in \{0,1\} & \forall i,j \in V
\end{aligned}
$$

引入变量$u_i$实现了subtour elimination,它要求随着hamilton tour中每个客户被访问的顺序的增加,其对应的$u_i$呈现递增，从而防止了subtour的形成，与Model 2的约束作用相同。


## Model 2

$x_{ij}$ = 1 if and only if the vehicle traverses the arc $(i, j)$.
$$
\begin{aligned}
\text{min} \quad & \sum_{i = 1}^{n}\sum_{j = 1}^n d_{ij}x_{ij} & \quad \\
\text{s.t.} \quad & \sum_{j = 1}^n x_{ij} = 1 & \forall i \in V \\
& \sum_{x = 1}^n x_{ij} = 1 & \forall j \in V \\
% subtour elimination
& \sum_{i \in S} \sum_{j \in S} x_{ij} \leq |S| - 1 & \forall S \subset V, 2 \leq |S| \leq n-1 \\
& x_{ij} \in \{0,1\} & \forall i,j \in V
\end{aligned}
$$

Model 2中的subtour elimination constraints will be tackled by `LazyConstraintsCallback`

