#  Largest Number At Least Twice of Others
------------------
@ [Description](https://leetcode.com/problems/largest-number-at-least-twice-of-others/)  
@ Tags: Array    
@ Easy

------------------
## Solution
```java
class Solution {
    public int dominantIndex(int[] nums) {
        if(nums == null || nums.length <= 1) return 0;
        int one = -1, two = -1, index = 0;
        for(int i = 0; i < nums.length; i++) {
            if(one < nums[i]) {
                two = one;
                one = nums[i];
                index = i;
            } else if (two < nums[i]) {
                two = nums[i];
            }
        }
        return one >= 2 * two ? index : -1;
    }
}
```
