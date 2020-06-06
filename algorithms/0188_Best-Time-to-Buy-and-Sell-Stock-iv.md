# Best Time to Buy and Sell Stock IV
------------------
@ [Description](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/)  
@ Tags: Array, DP   
@ Hard

------------------
## Solution - DP
$dp[i][j] = max(dp[i][j-1], max(dp[i-1][x] + price[j] - price[x]$for $x$ in $0$ to $j-1)$   
时间复杂度为$O(nk)$, 空间复杂度为$O(nk)$  
```java
class Solution {
    public int maxProfit(int k, int[] prices) {
        int l = prices.length;
        // make as many transactions as you can
        if (k >= l / 2) {
            int res = 0;
            for (int i = 1; i < l; i++) {
                if (prices[i] > prices[i - 1]) {
                    res += prices[i] - prices[i - 1];
                }
            }
            return res;
        }
        
        // maximum k transactions
        int[][] dp = new int[k + 1][l];
        for (int i = 1; i <= k; i++) {
            // pervious best
            int currBest = dp[i - 1][0] - prices[0];
            for (int j = 1; j < l; j++) {
                dp[i][j] = Math.max(dp[i][j - 1], prices[j] + currBest);
                // update pervious best, j will be used in j+1 round
                currBest = Math.max(currBest, dp[i - 1][j] - prices[j]);
            }
        }
        return dp[k][l - 1];
    }
}
```
