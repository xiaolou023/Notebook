# Preprocessing and Bounds

[TOC]

## Preprocessing

### Reduced set of possible packing points

**Normal patterns**

> reference: Côté, J. F., Dell’Amico, M., & Iori, M. (2014). Combinatorial benders’ cuts for the strip packing problem. Operations Research, 62(3), 643–661. https://doi.org/10.1287/opre.2013.1248

For strip packing problem, there is an optimal solution in which item is moved as down and as left as possible (then touching at its left, and its bottom,either the strip or the boarder of another item).

Therefore, the set of possible bottom-left points of items are **reduced to the set which is the combination of widths or heights of items**.
$$
\mathscr{W}(j)=\{p_{j}=\sum_{i \in \mathcal{N} \backslash\{j\}} w_{i} \xi_{i}: 0 \leqslant p_{j} \leqslant W-w_{j}, \xi_{i} \in\{0,1\}, \forall i \in \mathcal{N} \backslash\{j\}\} \\
\mathscr{H}(j)=\{r_{j}=\sum_{i \in \mathcal{N} \backslash\{j\}} h_{i} \xi_{i}: 0 \leqslant r_{j} \leqslant H-h_{j}, \xi_{i} \in\{0,1\}, \forall i \in \mathcal{N} \backslash\{j\}\}
$$

### Resort all the items

Before our algorithm, we sort all the items in the non-increasing order of width, breaking ties by non-increasing height.

### Resize the strip and rectangles

**reducing the width of strip**

It computes the maximum total width $\bar{W}$ of a subset of items that can be packed side by side without exceeding the strip width $W$ (by solving a standard subset sum problem), and then, if the resulting value is strictly smaller than $W$, it reduces the strip width by setting $W =\bar{W}$. 

**enlarging the width of rectangles**

It computes for any item $j$ in order the maximum total width $\bar{w}_j$ of a subset of items that can be packed side by side with $j$ without exceeding $W$ (again by solving a subset sum problem), and then, if  $w_j +\bar{w}_j <W$, it increases the item width by setting $w_j =W−\bar{w}_j$. (**no rotations**)

## Bounding Techniques

### Approximation

> No polynomial-time approximation algorithm for the BPP can have a WCPR smaller than $3/2$.

(1) sorting all the items according to **decreasing** weight;

(2) *first-fit* or *best-fit*: $3/2$

Algorithm *First-Fit (FF)* at each iteration into a new bin if it does not fit in any open bin. 

Algorithm *Best-Fit (BF)* at each iteration packs the next item into the feasible bin (if any) where it fits by leaving the smallest residual space, or into a new one if no open bin can accommodate it.

> FFD and BFD provide the best possible WCPR.

### strip packing problem

1. lower bound: the height of the tallest item
   $$
   L_{h}=\max _{j=1, \ldots, n}\left\{h_{j}\right\}
   $$
   
2. continuous lower bound
   $$
   L_{c}=\left\lceil\frac{\sum_{j \in J} w_{j} h_{j}}{W}\right\rceil
   $$
   
3. lower bound
   $$
   L_{0}=\max\{L_h, L_c\} = \max\{\max_{j \in \mathcal{N}} h_j, \left\lceil\sum_{j \in \mathcal{N}} w_{j} h_{j} / W\right\rceil\}.
   $$

4. combinatorial relaxation: one-dimensional bin packing problem with contiguity constraints.

5. combinatorial relaxation: resource constrained project scheduling problem, or multi-processor scheduling problem with contiguity constraints.



