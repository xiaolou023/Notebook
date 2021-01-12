# CP使用说明

[TOC]

## CP获取解的信息

`cp.getInfo(IloCP.IntInfo.NumberOfConstraints);`

获取约束的数目

`cp.getInfo(IloCP.IntInfo.NumberOfVariables);`

获取变量的数目

`cp.getStatus().toString();`

获取CP的求解状态

`cp.getObjValue()`

获取目标值（对于min问题，表现为上界）

`cp.getObjBound() `

获取目标值的bound（对于min问题，表现为下界）

## CP Functions

### 提供初始解：`setStartingPoint`

It pass a starting solution to the subsequent solving process of `CP` solver.

```java
IloSolution sp = cp.solution();
for (int i = 0; i < N; ++i) {
    sp.setStart(processTask[i], res.sol.s[i]);
    sp.setSize(processTask[i], res.sol.p[i]);
}
cp.setStartingPoint(sp);          
if (cp.solve()) {
    getResult(true);
    System.out.println(res.sol.s[N - 1]);
}
```

### Logical constraints

| Logical constraint            | Java API                            |
| :---------------------------- | :---------------------------------- |
| logical-and (conjunction)     | `IloModeler.and`                    |
| logical-or (disjunction)      | `IloModeler.or`                     |
| logical-not (negation)        | `IloModeler.not`                    |
| logical if-then (implication) | `IloModeler.ifThenIloCP.ifThenElse` |

