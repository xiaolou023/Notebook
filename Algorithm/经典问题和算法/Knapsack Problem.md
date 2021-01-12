# 0-1 Knapsack Problem

**Problem**

Given weights and values of n items, put these items in a knapsack of capacity W to get the maximum total value in the knapsack.

**Using dynamic programming**

$dp[i][w]$ represents the maximal value when items $0,1,\ldots, i$ are placed into a knapsack with capacity of $w$.

Base cases

$$
dp[0][w] = 0, dp[i][0] = 0
$$

Recursive formula

$$
dp[i][w] = \max\{dp[i-1,w],v_i + dp[i-1,w-w[i]\},\quad \forall 1 \leq i \leq n, 0 \leq w \leq W
$$

```java
public int solve_dp(){
    int[][] dp = new int[n + 1][W + 1];
    // Base cases
    for (int i = 0; i <= n; ++i)
        dp[i][0] = 0;
    for (int j = 0; j <= W; ++j)
        dp[0][j] = 0;
    // recusive formula
    for (int i = 1; i <= n; ++i) {
        for (int j = 1; j <= W; ++j) {
            if (wt[i - 1] > j) {
                dp[i][j] = dp[i - 1][j];
            }else {
                int temp = dp[i - 1][j - wt[i - 1]] + val[i - 1];
                dp[i][j] = Math.max(dp[i - 1][j], temp);
            }
        }
    }
    return dp[n][W];
}
```

**Using branch and bound**

```java
class HeapNode {
    double upbound; // 结点的价值上界
    double value; // 结点所对应的价值
    double weight; // 结点所相应的重量
 
    int level; // 活节点在子集树中所处的层序号
 
    public HeapNode() {
    }
}
 
// 分支限界法实现01背包问题
public class BB_Knapsack01 {
 
    int[] weight;
    int[] value;
    int max; // 背包的最大承重量
 
    int n;
 
    double c_weight; // 当前背包重量
    double c_value; // 当前背包价值
 
    double bestv; // 最优的背包价值
 
    Stack<HeapNode> heap;
 
    public BB_Knapsack01() {        
        weight = new int[] { 15, 16, 15, 0 };
        value = new int[] { 25, 45, 25, 0 };
        max = 30;
 
        n = weight.length - 1;
 
        c_weight = 0;
        c_value = 0;
        bestv = 0;
 
        heap = new Stack<HeapNode>();
    }
 
    // 求子树的最大上界
    private double maxBound(int t) {
        double left = max - c_weight;
        double bound = c_value;
        // 剩余容量和价值上界
        while (t < n && weight[t] <= left) {
            left -= weight[t];
            bound += value[t];
            t++;
        }
        if (t < n)
            bound += (value[t] / weight[t]) * left; // 装填剩余容量装满背包        
        return bound;
    }
 
    // 将一个新的活结点插入到子集树和最大堆heap中
    private void addLiveNode(double upper, double cvalue, double cweight,
            int level) {
        HeapNode node = new HeapNode();
        node.upbound = upper;
        node.value = cvalue;
        node.weight = cweight;
        node.level = level;
        if (level <= n)
            heap.push(node);
    }
 
    // 利用分支限界法，返回最大价值bestv
    private double knapsack() {
        int i = 0;
        double upbound = maxBound(i);
        // 调用maxBound求出价值上界，bestv为最优值
        while (true) // 非叶子结点        
        {
            double wt = c_weight + weight[i];
            if (wt <= max)// 左儿子结点为可行结点            
            {
                if (c_value + value[i] > bestv)
                    bestv = c_value + value[i];
                addLiveNode(upbound, c_value + value[i], c_weight + weight[i],
                        i + 1);
            }
            upbound = maxBound(i + 1);
            if (upbound >= bestv) // 右子树可能含最优解
                addLiveNode(upbound, c_value, c_weight, i + 1);
            if (heap.empty())
                return bestv;
            HeapNode node = heap.peek();
            // 取下一扩展结点
            heap.pop();
            //System.out.println(node.value + " ");
            c_weight = node.weight;
            c_value = node.value;
            upbound = node.upbound;
            i = node.level;
        }
    }
 
    public static void main(String[] args) {
        // TODO Auto-generated method stub
        BB_Knapsack01 knap = new BB_Knapsack01();
        double opt_value = knap.knapsack();
        System.out.println(opt_value);
    }
}
```

