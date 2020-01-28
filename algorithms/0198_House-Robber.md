# House Robber
------------------
@ [Description](https://leetcode.com/problems/house-robber/)  
@ Tags: DP     
@ Easy

------------------
## Solution
```java
class Solution {
    public int rob(int[] nums) {
        if(nums.length == 0) return 0;
        if(nums.length == 1) return nums[0];
        int dp[] = new int[nums.length];
        dp[0] = nums[0];
        dp[1] = Math.max(nums[1], nums[0]);
        for (int i = 2; i < nums.length; i++)
            dp[i] = Math.max(dp[i-1], nums[i] + dp[i-2]);
        return dp[nums.length - 1];
    }
}
```
其实只需记录前两个presum即可，可以优化储存空间。  
```java
class Solution {
    public int rob(int[] nums) {
        if(nums.length == 0) return 0;
        if(nums.length == 1) return nums[0];
        int prev = 0, prev2 = 0;
        for (int num : nums) {
            int temp = prev;
            prev = Math.max(prev2 + num, prev);
            prev2 = temp;
        }
        return prev;
    }
}
```
