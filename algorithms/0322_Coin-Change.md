# Coin Change
------------------
@ [Description](https://leetcode.com/problems/coin-change/)  
@ Tags: DP   
@ Medium

------------------
 # Solution
 时间复杂度：$O(SN)$  
 空间复杂度：$O(S)$  
 ```java
 class Solution {
    public int coinChange(int[] coins, int amount) {
        int[] dp = new int[amount + 1];
        Arrays.fill(dp, amount + 1);
        dp[0] = 0;
        for (int i = 1; i <= amount; i++) {
            for (int coin : coins) {
                if (coin <= i) 
                    dp[i] = Math.min(dp[i], dp[i-coin] + 1);
            }
        }
        return (dp[amount] > amount) ? -1 : dp[amount];
    }
}```
