# Traveling Salesman Problem (TSP)

## Lower Bounds

1. minimum weight 1 -tree
   
   **Spanning Tree**
   
   > A tree contains all the vertices of a graph $G$ is called the *spanning tree* of graph $G$.
   
   **Minimal Spanning Tree**
   
   > The spanning tree with least total edge weight over such tree.
   
   ![spanning trees](../../../Images/TSP_spanning_trees.jpg)
   
   **Minimum Spanning 1-Tree**

   > 在一个图$G(V,E)$中，节点集合$V = \{1...n\}$，我们定义$\{2...n\}$节点组成的子图的生成树以及两条与$\{1\}$节点的边组成的新图为1-tree.

   ![Minimum weight 1-tree](../../../Images/TSP_MinimumWeight1Tree.png)

   TSP的可行解是1-tree的一种，Minimum weight 1-tree 的最优值可以作为TSP的一个lower bound。求解minimum weight 1-tree的方法是：求解子图$\{2,\ldots, n\}$的最小生成树再加上两条与$\{1\}$节点相连的最短的边。
   
   一棵1-tree是一个TSP的可行解的充要条件是1-tree中所有节点的度(degree)均为2。
   
   
   
   
   
   
   
   
2. Assignment problem

