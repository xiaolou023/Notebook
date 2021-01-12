# Subset Sum Problem and Its Variants

**Problem 1**

> Given a set of non-negative integers, and a value *sum*, determine if there is a subset of the given set with sum equal to given *sum*.

> dynamic programming

Reference: https://www.geeksforgeeks.org/subset-sum-problem-dp-25/

```java
public boolean isSubetSum(int[] set, int target) {
    int n = set.length;
    boolean[][] dp = new boolean[n + 1][target + 1];
    // base cases
    for (int i = 0; i <= n; ++i)
        dp[i][0] = true;
    for (int j = 1; j <= target; ++j)
        dp[0][j] = false;
    for (int i = 1; i <= n; ++i) {
        for (int j = 1; j <= target; ++j) {
            if (dp[i-1][j])
                dp[i][j] = true;
            else
                if (set[i - 1] > j)
                    dp[i][j] = false;
                else
                    dp[i][j] = dp[i - 1][j - set[i - 1]];
        }
    }
    return dp[n][target];
}
```

**Problem 2**

> Given an array of integers and a sum. We have to find sum of subarray having maximum sum less than or equal to given sum in array.
>

Reference: https://www.geeksforgeeks.org/maximum-sum-subarray-sum-less-equal-given-sum/

*sliding window*

**Problem 3: Print sums of all subsets of a given set**

> Given an array of integers, print sums of all subsets in it. Output sums can be printed in any order.

Reference: https://www.geeksforgeeks.org/print-sums-subsets-given-set/

**Problem 4: Find all distinct subset (or subsequence) sums of an array**

> Given a set of integers, find distinct sum that can be generated from the subsets of the given sets and print them in an increasing order.

Reference: https://www.geeksforgeeks.org/find-distinct-subset-subsequence-sums-array/

