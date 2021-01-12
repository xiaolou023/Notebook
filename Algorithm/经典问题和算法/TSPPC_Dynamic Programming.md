## Travelling salesman problem with precedence constraints

Let $G=(V,A)$ be a directed graph, where $V=\{1,2,\ldots,n\}$ is the set of nodes/cities, $A$ is the arc set and $c_{ij}$ is the the traveling cost of each arc $(i,j) \in A$. A set of precedence relationships $(i,j) \in P$ is defined, meaning city $i$ must be visited prior to city $j$. This problem is to find the shortest possible route that satisfies the precedence constraints and visits each city exactly once. Let denote by 

This problem is a **NP-hard** problem.

```java
// backward dynamic programming
    public int solve_dp(int ub, int timelimit) {
        double timecost = 0;
        ArrayList<State> states = new ArrayList<>();
        State state0 = new State(new HashSet<>(), 0, 0);
        state0.route = "0";
        states.add(state0);
        int t = 1;
        while (t < n) {
            long t0 = System.currentTimeMillis();
            ArrayList<State> states_temp = new ArrayList<>();
            for (State state : states) {
                for (Integer j : getPrevNodes(state)) {
                    HashSet<Integer> jobs = new HashSet<>(state.jobs);
                    jobs.add(j);
                    State state_temp;
                    int index = find(states_temp, jobs, j);
                    if (index == -1)
                        state_temp = new State(jobs, j, Global.INF);
                    else
                        state_temp = states_temp.get(index);
                    if (t < n - 1) {
                        int temp = distance[j][state.i] + state.minCost;
                        if (temp < state_temp.minCost) {
                            state_temp.minCost = temp;
                            state_temp.route = j + " " + state.route;
                        }
                    } else {
                        int temp = distance[0][j] + distance[j][state.i] + state.minCost;
                        if (temp < state_temp.minCost) {
                            state_temp.minCost = temp;
                            state_temp.route = 0 + " " + j + " " + state.route;
                        }
                    }

                    if (index == -1)
                        states_temp.add(state_temp);
                }
            }
            states.clear();
            for (State state : states_temp) {
                if (state.minCost <= ub)
                    states.add(state);
            }
            t++;
            timecost += 0.001 * (System.currentTimeMillis() - t0);
            if (timecost > timelimit)
                break;
        }
        int cost = Global.INF;
        int index = 0;

        for (int i = 0; i < states.size(); i++) {
            State state = states.get(i);
            if (state.minCost < cost) {
                cost = state.minCost;
                index = i;
            }
        }

        // convert rt into route
        String[] temp = states.get(index).route.split("\\s+");
        for (int i = 0; i < temp.length; ++i)
            route[i] = Integer.parseInt(temp[i]);
        return cost;
    }
```



```java
    private boolean isFeasible(HashSet<Integer> jobs, int j) {
        if (jobs.contains(j))
            return false;
        if (jobs.size() < successors.get(j).size())
            return false;
        if (!jobs.containsAll(successors.get(j)))
            return false;

        return true;
    }

    private int find(ArrayList<State> states,  HashSet<Integer> jobs, int i) {
        for (int k = 0; k < states.size(); ++k) {
            State state = states.get(k);
            if (state.i == i && state.jobs.containsAll(jobs) && jobs.containsAll(state.jobs)) {
                return k;
            }
        }
        return -1;
    }

    private HashSet<Integer> getPrevNodes(State state) { // backward dp
        HashSet<Integer> set = new HashSet<>();
        for (int i = 0; i < n; i++) {
            if (isFeasible(state.jobs, i))
                set.add(i);
        }
        return set;
    }
}
```

