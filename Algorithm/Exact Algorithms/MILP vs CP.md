# MILP vs CP

Both MILP and CP frameworks rely on **branching** to explore the search tree. The primary difference lies in the way inference is performed at each node.

## Mixed Integer Linear Programming

Each node during search tree corresponds to a LP subproblem. A node is *fathomed* either when the objective value of LP relaxation is worse than the best integer solution obtained so far, the LP subproblem is infeasible. *Branching* is performed whenever the solution obtained by solving the LP relaxation does not satisfy all the constraints in the original problem. If the relaxed solution satisfies all the constraints in the original problem and is better than the best feasible solution found so far, then the best feasible solution is *updated*. The search *terminates* when it is proved that no better solution exists than the best feasible solution found.

The effectiveness of MILP methods depends on the size of the linear-programming subproblems, and more importantly, on the **gap** between the objective for the best feasible solution (optimum) and the objective function value obtained from the initial LP subproblem. There are a number of more sophisticated algorithms that focus on these aspects and use different ways of generating LP subproblems, like *Branch and Cut* and *Branch and Price* . These algorithms make use of *valid inequalities* to improve the performance of the solution algorithms.

## Constraint Programming

CP uses constraint propagation as the inference engine. At each node, constraint propagation is used to reduce the domains of all the variables. The domain of a variable can be continuous, discrete, boolean etc. Constraint propagation can result in empty domains in which case a node is *fathomed*. *Branching* is performed whenever the domain of a variable consists of more than one element (discrete and boolean domains) or the bounds are not within a certain tolerance (continuous domains). CP was originally developed to solve feasibility problems. <u>It has now been extended to solve optimization problems. This is achieved by solving a feasibility problem in which the objective function of the problem is rewritten as a constraint that forces it to be equal to a new variable. The domain of this new variable gives upper and lower bounds on the objective-function values.</u>  Whenever a feasible solution is obtained during the search, additional constraints that restrict the objective function values are imposed throughout the search tree. The search* terminate*s when all the nodes have been fathomed. The effectiveness of the CP methods depends primarily on the **constraint propagation algorithms** that are used to reduce the domain of a variable.

MILP has the advantage that the effect of all the constraints is evaluated simultaneously and it has a “Global Perspective” on all the constraints. CP, on the other hand, evaluates the effect of constraints sequentially by communicating through domains of the variables. When problems are loosely constrained, finding the optimal solution with CP may prove to be very difficult. 
CP methods have proved to be successful in solving highly constrained discrete optimization 
and feasibility problems for scheduling, configuration, and resource allocation.

## Reference

[^1]: Jain, V., & Grossmann, I. E. (2001). Algorithms for Hybrid MILP/CP Models for a Class of Optimization Problems. INFORMS Journal on Computing, 13(4), 258–276. https://doi.org/10.1287/ijoc.13.4.258.9733

