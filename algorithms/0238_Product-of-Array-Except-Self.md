# Product of Array Except Self
------------------
@ [Description](https://leetcode.com/problems/product-of-array-except-self/)  
@ Tags: Array  
@ Medium

------------------
## Solution
Two pass 的思想，第一遍遍历该index左边所有数乘积，然后再从尾部遍历右边所有数字乘积。  
时间复杂度：$O(N)$  
```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int[] res = new int[nums.length];
        res[0] = 1;
        for (int i = 1; i < nums.length; i++)
            res[i] = res[i - 1] * nums[i - 1];
        int right = nums[nums.length - 1];
        for (int i = nums.length - 2; i >= 0; i--) {
            res[i] *= right;
            right *= nums[i];
        }
        return res;
    }
}
```
