# Maximum Subarray
------------------
@ [Description](https://leetcode.com/problems/maximum-subarray/)  
@ Tags: Array, Divide and Conquer, Dynamic Programming    
@ Easy

------------------
 # Solution
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int max = nums[0], pre = nums[0];
        for (int i = 1; i < nums.length; i++) {
            pre = Math.max(nums[i], nums[i] + pre);
            max = Math.max(max, pre);
        }
        return max;
    }
}
```
