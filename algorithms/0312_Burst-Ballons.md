# Burst Balloons
------------------
@ [Description](https://leetcode.com/problems/burst-balloons/)  
@ Tags: Divide and Conquer, DP   
@ Hard

------------------
## Solution 1 - DP
逆向思维，dp[i][j]表示从i到j的序列的最大值，那么我们最终结果即为dp[1][n]。如果我们考虑第k个元素是我们最后一个打破的，那么dp[i][j] = max(dp[i][j], dp[i][k-1] + nums[i-1]*nums[k]*nums[j+1] + dp[k+1][j]).  
时间复杂度$O(n^3)$  
空间复杂度$O(n^2)$  
```java
class Solution {
    public int maxCoins(int[] nums) {
        int n = nums.length;
        // pad the nums array
        int[] pad_nums = new int[n + 2];
        pad_nums[0] = 1;
        pad_nums[n + 1] = 1;
        for (int i = 0; i < n; i++) {
            pad_nums[i + 1] = nums[i];
        }
        
        // dp
        int[][] dp = new int[n + 2][n + 2];
        // iterate from length 1 to n
        for (int l = 1; l <= n; l++) {
            for (int i = 1; i + l - 1 <= n; i++) {
                int j = i + l - 1;
                for (int k = i ; k <= j; k++) {
                    dp[i][j] = Math.max(dp[i][j], dp[i][k-1] + dp[k+1][j] + pad_nums[i-1] * pad_nums[k] * pad_nums[j+1]);
                }
            }
        }
        return dp[1][n];
    }
}
```

## Solution 2 - Divid and Conquer
```java
class Solution {
    public int maxCoins(int[] nums) {
        int n = nums.length;
        int[] pad_nums = new int[n + 2];
        pad_nums[0] = 1;
        pad_nums[n + 1] = 1;
        for (int i = 0; i < n; i++) {
            pad_nums[i + 1] = nums[i];
        }
        int[][] dp = new int[n + 2][n+2];
        return helper(1, n, pad_nums, dp);   
    }
    
    private int helper(int start, int end, int[] nums, int[][] dp) {
        // if value is not 0, means the value has already been update
        if (dp[start][end] != 0) {
            return dp[start][end];
        }
        for (int i = start; i <= end; i++) {
            int left = helper(start, i - 1, nums, dp);
            int right = helper(i + 1, end, nums, dp);
            dp[start][end] = Math.max(dp[start][end], left + nums[start - 1] * nums[i] * nums[end + 1] + right);
        }
        return dp[start][end];
    }
}
```
