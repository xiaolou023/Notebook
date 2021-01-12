# Branch and Bound

**如何设计branch and bound?**

+ **Node**

  Node的含义是什么？Node有哪些属性和方法？
  
  Node的含义和solution representation (decoder)有关。例如：在TSP中,每个solution可以表示为sequence of nodes,那么在search tree中,每个node即为partial sequence of nodes,对应于partial solution。

  对于optimization problem, node的属性通常包括`seq`, `lb`,`ub`,`parent`。node的方法则包括`makeChildren()`,`computeUB()`,`computeLB()`,`isComplete()`。

+ **Branching rule**

    对应Node的`makeChildren()`,指的是如何创建子结点、如何分支。例如：in rectangular packing problem, a branching operation considers all possible packing positions of all unpacked rectangles.

+ **Node selection**

    指的是在branch之后,如何选择下一个Node。可以在添加子结点时保持一定顺序，取出时顺序取出，也可以在添加子节点时任意顺序，取出时保持一定顺序。
    
    Branch and Bound的实现是围绕搜索树展开的，所以Node selection的顺序对应着搜索树的搜索顺序。

    常考虑的策略有：breadth-first search, depth first search, best-first search。

    BFS可以通过`FIFO Queue`实现, DFS可以通过`LIFO Queue`实现, Best-first search是一种启发式搜索算法（Heuristic Algorithm），其基于广度优先搜索算法，不同点是其依赖于估价函数对将要遍历的节点进行估价，选择代价小的节点进行遍历，直到找到目标点为止。这种搜索可以用优先队列priority queue来实现。

    即使是在depth first search中, 也可以通过自定义的scoring()给各个node评分从而有不同的node selection。
    例如：in rectangular packing problem, we consider the placement(rectangle, position) by non-decreasing *fitness number*, ties broken by decreasing area.

+ **Bounding operation**

    指的是如何判断是否还需要继续分支——当此节点不可行,或者没有希望超过当前最优解时,回溯。当此节点得到更好的解时，更新全局最优解。

## Framework of Branch and Bound

```pseudocode
1. Using a heuristic, find a solution $x_h$ to the **minimization** problem. Store its value, $B = f(x_h)$. (If no heuristic is available, set $B$ to infinity.) $B$ will denote the best solution found so far, and will be used as an upper bound on candidate solutions.

2. Initialize a queue (or stack) to hold a partial solution with none of the variables of the problem assigned.

3. Loop until the queue is empty:

    3.1. Take a node $N$ off the queue.
    
    3.2. If $N$ represents a complete candidate solution $x$ and $f(x) < B$, then $x$ is the best solution so far. Record it and set $B \gets f(x)$.
    
    3.3. Else, branch on $N$ to produce new child nodes $N_i$. For each of these:

       3.3.1. If lower bound $(N_i) > B$, fathome the node $N_i$; since the lower bound on this node is greater than the upper bound of the problem, it will never lead to the optimal solution, and can be discarded.
    
       3.3.2. Else, store $N_i$ on the queue.
```

```java
Branch and Bound for Minimization Problem
procedure bnb():
int best = heur(); // set the best UB so far
Stack<Node> stack= new Stack<Node>(); // stack stores all candidate nodes
Node node = root(); // create the root node
stack.push(node);

while (!stack.isEmpty()) do
    node = stack.pop(); // DFS
    if (node.isComplete()) then // node provides a complete solution
        if (node.obj < best) then
            best = node.obj;
            record the current node;
        end
    else if (node.LB $\leq$ best) then
        	ArrayList<Node> children = node.makechilden(); // make new child nodes
        	for (Node child : children) do
            	if (child.LB $\leq$ best) then
                	stack.push(child);
            	end // fathome those LB > best & infeasible nodes
        	end
        end
    end
end
```