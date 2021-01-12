# CPLEX使用说明

[TOC]

## CPLEX的解法池solution pool

Cplex的解法池允许生成并存储MIP model的多个解。

- [可以选择仅收集一定质量（gap）的解](https://www.ibm.com/support/knowledgecenter/zh/SSSA5P_12.7.0/ilog.odms.cplex.help/CPLEX/Parameters/topics/SolnPoolGap.html)  `IloCplex.Param.MIP.Pool.RelGap`
- [可以控制解法池解替代的方式](https://www.ibm.com/support/knowledgecenter/zh/SSSA5P_12.7.0/ilog.odms.cplex.help/CPLEX/Parameters/topics/SolnPoolReplace.html)  `IloCplex.Param.MIP.Pool.Replace`
- [可以控制解池中解的差异性](https://www.ibm.com/support/knowledgecenter/zh/SSSA5P_12.7.0/ilog.odms.cplex.help/CPLEX/UsrMan/topics/discr_optim/soln_pool/38_diversity_filters.html)  `IloCplex.addDiversityFilter`
- [指定在解池中存储的解的数量](https://www.ibm.com/support/knowledgecenter/zh/SSSA5P_12.7.0/ilog.odms.cplex.help/CPLEX/Parameters/topics/SolnPoolCapacity.html) `IloCplex.Param.MIP.Pool.Capacity`

### [解法池中添加新解](https://www.ibm.com/support/knowledgecenter/zh/SSSA5P_12.7.0/ilog.odms.cplex.help/CPLEX/UsrMan/topics/discr_optim/soln_pool/04_filling.html)

- 累积连续现任解 `accumulate`

  当用solve()求解MIP model时，它会在发现现任解时向解池自动添加这些现任解。

- 填充 ` populate`

### [枚举所有解法](https://www.ibm.com/support/knowledgecenter/zh/SSSA5P_12.7.0/ilog.odms.cplex.help/CPLEX/UsrMan/topics/discr_optim/soln_pool/18_howTo.html)

| 用途               | Concert Technology      | Interactive Optimizer |
| :----------------- | :---------------------- | :-------------------- |
| 解法数量           | getSolnPoolNsolns       | display solution pool |
| 已替换数量         | getSolnPoolNreplaced    | display solution pool |
| 目标值的算术平均值 | getSolnPoolMeanObjValue | display solution pool |

- 访问解法池解法 `getSolnPoolNsolns`

  如果要访问解法池中可用的所有解法，那么应从0到N-1进行循环（即，池中的解法数减一）。 索引0在传统上是指当前现任解法。

- 写入解法 `writeSolution`, `writeSolutions `

- 删除解法  `delSolnPoolSolns`   

## CPLEX获取所有最优解

Reference: [Using CPLEX to examine alternate optimal solutions](https://www.ibm.com/support/pages/using-cplex-examine-alternate-optimal-solutions)

[It could be achieved, but complex.]

方法一：solution pool

方法二：修改目标函数或者约束，排除当前最优解。

## CPLEX获取MIP的LP relaxation

```
cplex.setParam(IloCplex.Param.MIP.Limits.Node, 0);
cplex.solve();
```

## CPLEX Functions

### `setPriority`

设置分支的优先顺序。如果不声明则默认为0，拥有高优先级编号的变量具有更高的分支优先权。

### `setDirection`

指定分支方向

| Parameter | Meaning                                                      |
| --------- | ------------------------------------------------------------ |
| `Up`      | process the child where the lower bound of the variable has been tightened first (e.g., > 4.3) |
| `Down`    | process the child where the upper bound of the variable has been tightened first (e.g., < 4.3) |
| `Global`  | process the child first that the MIP optimizer would have ordinarily chosen |

### `MIPDisplay`

控制`CPLEX`在日志文件中记录和显示信息的方式

```java
cplex.setParam(IloCplex..IntParam.MIPDisplay, 1);
```

```java
cplex.setOut(null);
cplex.setWarning(null);
```

| Value | Meaning                                                      |
| :---- | :----------------------------------------------------------- |
| 0     | No display until optimal solution has been found             |
| 1     | Display integer feasible solutions                           |
| 2     | Display integer feasible solutions plus an entry at a frequency set by [MIP node log interval](https://www.ibm.com/support/knowledgecenter/SSSA5P_12.8.0/ilog.odms.cplex.help/CPLEX/Parameters/topics/MIPInterval.html?view=kc); **default** |
| 3     | Display the number of cuts added since previous display; information about the processing of each successful MIP start; elapsed time in seconds and elapsed time in deterministic ticks for integer feasible solutions |
| 4     | Display information available from previous options and information about the LP subproblem at root |
| 5     | Display information available from previous options and information about the LP subproblems at root and at nodes |

### `IloNumVarType`

CPLEX中的变量的类型：`Bool`，`Int`，`Float`

### `MIPEmphasis`

[Emphasizing feasibility and optimality](https://www.ibm.com/support/knowledgecenter/en/SSSA5P_12.7.0/ilog.odms.cplex.help/CPLEX/UsrMan/topics/discr_optim/mip/usage/10_emph_feas.html)

Emphasizing feasibility and optimality: `Balanced(DEFAULT)`, `Optimality`, `Feasibility`,, `BestBound`, `HiddenFeas`.

Optimizing a MIP model involves: finding a succession of improving integer feasible solutions (that is, solutions satisfying the linear and quadratic constraints and the integrality conditions); while also working toward a proof that no better feasible solution exists and is undiscovered.

| Field | Description                                     |
| :---------------- | :-------------------------------------------------------- |
| `Balanced`      |  Balance optimality and feasibility.            |
| `Optimality`     |  Optimality over feasibility.                 |
| `Feasibility`      |  Feasibility over optimality.                |
| `BestBound`      |  Emphasize moving best bound.                  |
| `HiddenFeas`      | Emphasize finding hidden feasible solutions. |

### `addMIPStart`

[IBM: Starting from a solution-MIP starts](https://www.ibm.com/support/knowledgecenter/en/SSSA5P_12.7.0/ilog.odms.cplex.help/CPLEX/UsrMan/topics/discr_optim/mip/para/49_mipStarts.html)

```java
IloNumVar[] startVar = new IloNumVar[m * n];
double[] startVal = new double[m * n];
for (int i = 0, idx = 0; i < m; ++i)
      for (int j = 0; j < n; ++j) {
          startVar[idx] = x[i][j];
          startVal[idx] = start[i][j];
          ++idx;
       }
cplex.addMIPStart(startVar, startVal);
startVar = null;
startVal = null;
```

### `importModel` & `exportModel`

`importModel`: read model from a file

`exportModel`: export model to a file