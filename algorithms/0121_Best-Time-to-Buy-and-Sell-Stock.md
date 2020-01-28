# Best Time to Buy and Sell Stock
------------------
@ [Description](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)  
@ Tags: Arrays, DP     
@ Easy

------------------
## Solution
```java
class Solution {
    public int maxProfit(int[] prices) {
        int min = Integer.MAX_VALUE;
        int res = 0;
        for (int i = 0; i < prices.length; i++) {
            if (prices[i] - min > res)
                res = prices[i] - min;
            min = Math.min(min, prices[i]);
        }
        return res;
    }
}
```
