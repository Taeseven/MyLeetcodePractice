#  Best Time to Buy and Sell Stock II
------------------
@ [Description](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)  
@ Tags: Array, Greedy   
@ Easy

------------------
## Solution - DP
状态转换，时间复杂度为$O(n)$, 空间复杂度为$O(1)$  
```java
class Solution {
    public int maxProfit(int[] prices) {
        int hold = Integer.MIN_VALUE;
        int sold = 0;
        
        for (int price : prices) {
            int preHold = hold;
            hold = Math.max(hold, sold - price);
            sold = Math.max(sold, preHold + price);
        }
        return sold;
    }
}
```
