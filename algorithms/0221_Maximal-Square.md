# Maximal Square
------------------
@ [Description](https://leetcode.com/problems/maximal-square/)  
@ Tags: DP     
@ Medium

------------------
## Solution
利用DP的思想从左上向右下遍历。  
当前值若为0，则当前可构成的正方形边长一定为0；  
若当前值为1，则当前位置可以构成的最大正方形取决于左、左上和上三个方向元素的最小值。  
```java
class Solution {
    public int maximalSquare(char[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0)
            return 0;
        int m = matrix.length, n = matrix[0].length;
        int[][] dp = new int[m+1][n+1];
        int max = 0;
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (matrix[i-1][j-1] == '0')
                    dp[i][j] = 0;
                else {
                    dp[i][j] = Math.min(dp[i-1][j], Math.min(dp[i-1][j-1], dp[i][j-1])) + 1;
                }
                max = Math.max(max, dp[i][j]);
            }
        }
        return max * max;
    }
}
```
