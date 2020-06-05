# Best Time to Buy and Sell Stock with Transaction Fee
------------------
@ [Description](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)  
@ Tags: Array, Greedy, DP   
@ Medium

------------------
## Solution - DP
状态转换，时间复杂度为$O(n)$, 空间复杂度为$O(1)$  
```java
class Solution {
    public int maxProfit(int[] prices, int fee) {
        // use MIN_VALUE may cause overflow
        int hold = -50000;
        int sold = 0;
        
        for (int price : prices) {
            int preHold = hold;
            hold = Math.max(hold, sold - price);
            sold = Math.max(sold, preHold + price - fee);
        }
        return sold;
    }
}
```
