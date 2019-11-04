# Minimum Path Sum
------------------
@ [Description](https://leetcode.com/problems/minimum-path-sum/)  
@ Tags: Array, DP     
@ Medium

------------------
## Solution - DP
只需要两行储存即可。
```java
class Solution {
    public int minPathSum(int[][] grid) {
        if (grid == null || grid.length == 0 || grid[0].length == 0)
            return 0;
        int[][] dp = new int[2][grid[0].length];
        dp[0][0] = grid[0][0];
        for (int i = 1; i < grid[0].length; i++)
            dp[0][i] = dp[0][i-1] + grid[0][i];
        for (int i = 1; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (j == 0)
                    dp[1][j] = dp[0][j] + grid[i][j];
                else
                    dp[1][j] = Math.min(dp[1][j-1], dp[0][j]) + grid[i][j];
            }
            dp[0] = dp[1];
        }
        return dp[0][grid[0].length - 1];
    }
}
```
