# Remove Element
------------------
@ [Description](https://leetcode.com/problems/remove-element/)  
@ Tags: Array, Two Pointers  
@ Easy 

------------------
## Solution
```java
class Solution {
    public int removeElement(int[] nums, int val) {
        if (nums == null || nums.length == 0)
            return 0;
        int l = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != val)
                nums[l++] = nums[i];
        }
        return l;
    }
}
```
