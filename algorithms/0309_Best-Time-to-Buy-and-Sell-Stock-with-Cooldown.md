# Best Time to Buy and Sell Stock with Cooldown
------------------
@ [Description](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)  
@ Tags: DP   
@ Medium

------------------
## Solution - DP
可以理解为三个状态的互相转换，[视频](https://www.youtube.com/watch?v=oL6mRyTn56M)。  
时间复杂度$O(n)$, 空间复杂度$O(1)$  
```java
class Solution {
    public int maxProfit(int[] prices) {
        int rest = 0, sold = 0;
        int hold = Integer.MIN_VALUE;
        
        for (int price : prices) {
            int preRest = rest;
            rest = Math.max(rest, sold);
            sold = hold + price;
            hold = Math.max(hold, preRest - price);
        }
        return Math.max(rest, sold);
    }
}
```
