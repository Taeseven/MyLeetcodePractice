# Minimum Size Subarray Sum
------------------
@ [Description](https://leetcode.com/problems/minimum-size-subarray-sum/)  
@ Tags: Array, Two Pointers, Binary Search    
@ Medium

------------------
## Solution
Two pointer, 时间复杂度：$O(N)$  
```java
class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        int i = 0, j = 0;
        int res = Integer.MAX_VALUE;
        int sum = 0;
        while (i < nums.length) {
            while (j < nums.length && sum < s) {
                sum += nums[j];
                j++;
            }
            if (sum >= s)
                res = Math.min(j - i, res);
            sum -= nums[i];
            i++;
        }
        return (res != Integer.MAX_VALUE) ? res : 0;
    }
}
```
