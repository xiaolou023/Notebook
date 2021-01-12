# TSP: Dynamic programming

## Travelling salesman problem

Given a set of cities and distance between every pair of cities, the problem is to find the shortest possible route that visits every city exactly once and returns to the starting point.

This problem is a **NP-hard** problem.

## Dynamic programming

Supposing we start from node $o$ and return to node $o$ finally. Here are $n$ nodes. (the optimal objective value is same no matter which node we start from.)

**状态**

$d(i, V')$ represents the minimal distance starting from node $i$ and traverse all the nodes in set $V'$ and then returns to node $o$.

**状态转移方程**

- $d(o,o) = 0$
- $d(i,V'\cup \{i\}) = \text{min}_{ k \in V'}\{d_{ik} + d(k, V')\} $

**目标函数**

$\text{min}_{i \in S}\{d(i, S) + d_{oi}\}$ where $S$ is a set including all the nodes.

**时间复杂度**

$2^n$

**Tips**

We need an array $dp[n][2^n]$ to record the minimal distance during the search process.

$dp[i][j]$: $i$ represents the current node $i$,  and $j$ represents the set of nodes $V'$ that is represented by a binary format.

**循环实现的DP**

```java
int solve_loop(int n, int[][] distance) {
    int b = 1 << (n - 1);
    int dp = new int[n][b];
    String route = new String[n][b];
    for (int i = 0; i < n; ++i) { // initialization
        dp[i][0] = distance[i][0];
        for (int j = 1; j < b; ++j) {
            dp[i][j] = Global.INF;
            route[i][0] = i + " 0";
        }
    }

    for (int j = 1; j < b; ++j) { // all sets S
        for (int i = 0; i < n; ++i){
            if(((1 << (i - 1)) & j) == 0) { // all i \notin S
                for (int k = 1; k < n; ++k) {
                    if (((1 << (k - 1)) & j) != 0) { // all k \in S
                        int temp = distance[i][k] + dp[k][j ^ (1 << (k - 1))];
                        if (temp < dp[i][j]) {
                            dp[i][j] = temp;
                            route[i][j] = i + " " + route[k][j ^ (1 << (k - 1))];
                        }
                    }
                }
            }
        }
    }
    System.out.println("minimal total distance: " + dp[0][b - 1]);
    System.out.println("minimal route: " + route[0][b - 1]);
    return dp[0][b-1];
}
```

**递归实现的DP** (存在bugs)

```c
#include <iostream>
using namespace std;
int N = 16;	// number of nodes
int b = 1 << (N - 1);
int Map[N][N];
int dp[N][b];	//dp[cur][status]

// the number of 1, is the number of cities visited
int num_of_1(int status) {	
	int n = status;
    int sum = 0;
    while (n != 0) {
    	sum++;
    	n = (n - 1) & n;
    }
    return sum;
}

// culculates the minimal length
int get(int cur,int status) {
	if(dp[cur][status]!=-1) {
		return dp[cur][status];
	}
	if (num_of_1(status)>2){ // more than two nodes
		int t=2;
		int minlen=10000000;
		for (int i=1;i<N;++i,t<<=1) {
			if (i==cur)
				continue;
			if ((status & t) !=0 ) {
                int temp = get(i,status & (~(1<<cur)));
				if (temp + Map[cur][i] < minlen) {	//去掉当前位
					minlen=temp + Map[cur][i];
				}
			}
		}
		return dp[cur][status]=minlen;
	}else { // returns to depot (only two nodes)
		return dp[cur][status]=Map[0][cur];
	}	
}
int main()
{
	int minlen;
	if (N==1) {
		return 0;
	}
   
	for (i=0;i<N;++i) {
		for (j=0;j<b;++j) {
			dp[i][j]=-1; // initialize
		}
	}
	dp[0][1]=0;		//处在第一个点，即出发点
	minlen=10000000;
	for (i=1;i<N;++i) {
        int temp = get(i,(1<<N)-1);
		if (Map[0][i]+get(i,(1<<N)-1)<minlen) {
			minlen=Map[0][i]+temp;
		}
	}
	cout<<minlen<<endl;
}
```



