# Best Time to Buy and Sell Stock III
------------------
@ [Description](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/)  
@ Tags: Array, DP   
@ Hard

------------------
## Solution - DP
状态转换，时间复杂度为$O(n)$, 空间复杂度为$O(1)$  
```java
class Solution {
    public int maxProfit(int[] prices) {
        int hold1 = Integer.MIN_VALUE;
        int hold2 = Integer.MIN_VALUE;
        int sold0 = 0, sold1 = 0, sold2 = 0;
        
        for (int price : prices) {
            int preHold1 = hold1;
            int preHold2 = hold2;
            hold1 = Math.max(hold1, sold0 - price);
            hold2 = Math.max(hold2, sold1 - price);
            sold1 = Math.max(sold1, preHold1 + price);
            sold2 = Math.max(sold2, preHold2 + price);
        }
        return Math.max(sold1, sold2);
    }
}
```
