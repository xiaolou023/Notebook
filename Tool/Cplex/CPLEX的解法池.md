# CPLEX的解法池solution pool

Cplex的解法池允许生成并存储MIP model的多个解。

- [可以选择仅收集一定质量（gap）的解](https://www.ibm.com/support/knowledgecenter/zh/SSSA5P_12.7.0/ilog.odms.cplex.help/CPLEX/Parameters/topics/SolnPoolGap.html)  `IloCplex.Param.MIP.Pool.RelGap`

- [可以控制解法池解替代的方式](https://www.ibm.com/support/knowledgecenter/zh/SSSA5P_12.7.0/ilog.odms.cplex.help/CPLEX/Parameters/topics/SolnPoolReplace.html)  `IloCplex.Param.MIP.Pool.Replace`

- [可以控制解池中解的差异性](https://www.ibm.com/support/knowledgecenter/zh/SSSA5P_12.7.0/ilog.odms.cplex.help/CPLEX/UsrMan/topics/discr_optim/soln_pool/38_diversity_filters.html)  `IloCplex.addDiversityFilter`

- [指定在解池中存储的解的数量](https://www.ibm.com/support/knowledgecenter/zh/SSSA5P_12.7.0/ilog.odms.cplex.help/CPLEX/Parameters/topics/SolnPoolCapacity.html) `IloCplex.Param.MIP.Pool.Capacity`

## 解法池中添加新解

- 累积连续现任解 `accumulate`

  当用solve()求解MIP model时，它会在发现现任解时向解池自动添加这些现任解。

- 填充 ` populate`

## 枚举所有解法

| 用途               | Concert Technology      | Interactive Optimizer |
| :----------------- | :---------------------- | :-------------------- |
| 解法数量           | getSolnPoolNsolns       | display solution pool |
| 已替换数量         | getSolnPoolNreplaced    | display solution pool |
| 目标值的算术平均值 | getSolnPoolMeanObjValue | display solution pool |

- 访问解法池解法 `getSolnPoolNsolns`

  如果要访问解法池中可用的所有解法，那么应从0到N-1进行循环（即，池中的解法数减一）。 索引0在传统上是指当前现任解法。

- 写入解法 `writeSolution`, `writeSolutions `

- 删除解法  `delSolnPoolSolns`   

