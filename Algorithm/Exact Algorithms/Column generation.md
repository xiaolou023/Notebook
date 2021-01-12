# Column Generation

参考*Chapter 6. Introduction to Linear Optimization*

Column Generation是Branch and Bound的基础。

# Column Generation求解Cutting Stock Problem

## Cutting Stock Problem

> 木材厂卖木材，某顾客需要25根3英尺的木材、20根5英尺的木材和15根9英尺的木材，木材厂通过切17英尺的木材来满足顾客的需求。目标最小化需要的木材数量。

```java
package ora;

import ilog.concert.*;
import ilog.cplex.IloCplex;

/**
 * Example of Column Generation: Cutting Stock Problem
 * @author by Ying
 * @version 2020/3/7
 */
public class CutStock {
    private int roll_width;
    private int[] item_width;
    private int[] item_demand;
    private int nTypes;

    public CutStock(int roll_width, int[] item_width, int[] item_demand) {
        this.roll_width = roll_width;
        this.item_width = item_width;
        this.item_demand = item_demand;
        this.nTypes = item_width.length;
    }

    // solve CSP with column generation
    public void solve_CG() {
        try {
            Master master = new Master();
            Slave slave = new Slave();
            while (true) {
                // optimize over current patterns
                master.solve();
                master.report();
                // find a new pattern to enter the basis
                slave.setObjExpr(master);
                slave.solve();
                slave.report();
                // optimality
                if (slave.getObjVal() >= -Global.EPS)
                    break;
                master.addColumn(Global.toIntegers(slave.getValues()));
            }
            master.convertToMip(); // solve MIP
            master.solve();
            master.reportSol();
            master.close();
            slave.close();
        } catch (IloException e) {
            e.printStackTrace();
        }
    }

    // master problem: cutting optimization problem
    // model by columns
    class Master {
        private IloCplex solver;
        private IloObjective roll_used;
        private IloRange[] fill;
        private IloNumVarArray patterns;

        Master() throws IloException {
            formulate();
        }

        private void formulate() throws IloException {
            solver = new IloCplex();
            roll_used = solver.addMinimize();
            fill = new IloRange[nTypes];
            patterns = new IloNumVarArray(); // ArrayList<IloNumVar>

            for (int i = 0; i < nTypes; i++) {
                fill[i] = solver.addRange(item_demand[i], Double.MAX_VALUE);
            }
            // the following model begins with an initial basis,
            // e.g., each roll is partitioned into only one
            // kind of smaller rolls each time
            for (int i = 0; i < nTypes; i++) {
                // create a new variable (i.e., column, or pattern)
                IloColumn col = solver.column(roll_used, 1.0);
                col = col.and(solver.column(fill[i], roll_width / item_width[i]));
                IloNumVar var = solver.numVar(col, 0, Double.MAX_VALUE);
                patterns.add(var);
            }
        }

        void addColumn(int[] pattern) throws IloException {
            IloColumn col = solver.column(roll_used, 1);
            for (int i = 0; i < nTypes; i++) {
                col = col.and(solver.column(fill[i], pattern[i]));
            }
            patterns.add(solver.numVar(col, 0, Double.MAX_VALUE));
        }

        void convertToMip() throws IloException {
            for (int i = 0; i < patterns.getSize(); i++) {
                solver.add(solver.conversion(patterns.getElement(i),
                        IloNumVarType.Int));
            }
        }

        void solve() throws IloException {
            // algorithm for LP relaxation
            solver.setParam(IloCplex.Param.RootAlgorithm,
                    IloCplex.Algorithm.Primal);
            solver.setOut(null);
            solver.solve();
        }

        void report() throws IloException {
            System.out.println("Using " + solver.getObjValue() + " rolls");
            // get value: number of rolls used for each pattern
            for (int i = 0; i < patterns.getSize(); i++) {
                System.out.println("Pattern " + i + " = " +
                        solver.getValue(patterns.getElement(i)));
            }
            // get dual variable
            for (int i = 0; i < nTypes; i++) {
                System.out.println("Fill " + i + " = " +
                        solver.getDual(fill[i]));
            }
            System.out.println();
        }

        void reportSol() throws IloException {
            System.out.println("Best integer solution uses " +
                    solver.getObjValue() + " rolls");
            for (int i = 0; i < patterns.getSize(); i++) {
                System.out.println("Pattern " + i + " = " + solver.getValue(patterns.getElement(i)));
            }
            System.out.println("Solution status: " + solver.getStatus());
        }

        void close() {
            solver.end();
        }
    }

    // slave problem: compute the least reduced cost
    // find a column to enter the basis
    class Slave {
        private IloCplex solver;
        private IloObjective reduced_cost;
        private IloNumVar[] item_used;

        Slave() throws IloException {
            formulate();
        }

        private void formulate() throws IloException {
            solver = new IloCplex();
            reduced_cost = solver.addMinimize();
            item_used = solver.intVarArray(nTypes, 0, Integer.MAX_VALUE);
            solver.addLe(solver.scalProd(item_width, item_used), roll_width);
        }

        void setObjExpr(Master master) throws IloException {
            double[] prices = master.solver.getDuals(master.fill).clone();
            IloNumExpr expr = solver.diff(1, solver.scalProd(item_used, prices));
            reduced_cost.setExpr(expr);
        }

        double getObjVal() throws IloException {
            return solver.getObjValue();
        }

        double[] getValues() throws IloException {
            return solver.getValues(item_used).clone();
        }

        void solve() throws IloException {
            solver.setOut(null);
            solver.solve();
        }

        void report() throws IloException {
            System.out.println("Minimum reduced cost is " + solver.getObjValue());
            if (solver.getObjValue() <= -Global.EPS) {
                for (int i = 0; i < nTypes; i++) {
                    System.out.println("Use " + i + " = " + solver.getValue(item_used[i]));
                }
            }
            System.out.println();
        }

        void close() {
            solver.end();
        }
    }

    class IloNumVarArray {
        private int cnt = 0;
        private IloNumVar[] array = new IloNumVar[32];

        void add(IloNumVar var) {
            if (cnt >= array.length) {
                IloNumVar[] array = new IloNumVar[2 * this.array.length];
                System.arraycopy(this.array, 0, array, 0, cnt);
                this.array = array;
            }
            array[cnt++] = var;
        }

        IloNumVar getElement(int i) {
            return array[i];
        }

        int getSize() {
            return cnt;
        }
    }
}
```


