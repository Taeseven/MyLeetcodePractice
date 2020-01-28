# Unique Binary Search Trees
------------------
@ [Description](https://leetcode.com/problems/unique-binary-search-trees/)  
@ Tags: DP, Tree     
@ Nedium

------------------
## Solution
注意BST的结构，根据根节点的不同左右子树所包含的node数的关系。
```java
class Solution {
    public int numTrees(int n) {
        if (n < 1) return 0;
        int[] dp = new int[n + 1];
        dp[0] = 1;
        dp[1] = 1;
        for (int i = 2; i <= n; i++) {
            for (int j = 0; j < i; j++) 
                dp[i] += dp[j] * dp[i - j - 1];
        }
        return dp[n];
    }
}
```
