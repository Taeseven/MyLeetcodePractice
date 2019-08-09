# Remove Duplicates from Sorted Array
------------------
@ [Description](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)  
@ Easy 

------------------
## Solution
```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int len = nums.length;
        if (len < 2) return len;
        int tail = 0;
        for (int i = 1; i < nums.length; i++) {
            if (nums[tail] != nums[i]) nums[++tail] = nums[i];
        }
        return tail + 1;
    }
}
```
