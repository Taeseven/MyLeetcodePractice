# Maximum Product Subarray
------------------
@ [Description](https://leetcode.com/problems/maximum-product-subarray/)  
@ Tags: DP, Array    
@ Nedium

------------------
## Solution
Loop through the array, each time remember the max and min value for the previous product, the next max and min value will depend on the previous ones and then the most important thing is to update the max and min value.
```java
class Solution {
    public int maxProduct(int[] nums) {
        if (nums == null || nums.length == 0)
            return 0;
        int max = nums[0], min = nums[0], res = nums[0];
        for (int i = 1; i < nums.length; i++) {
            int temp = max;
            max = Math.max(nums[i], Math.max(max * nums[i], min * nums[i]));
            min = Math.min(nums[i], Math.min(temp * nums[i], min * nums[i]));
            res = Math.max(res, max);
        }
        return res;
    }
}
```
