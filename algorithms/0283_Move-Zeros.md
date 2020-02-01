#  Move Zeros
------------------
@ [Description](hhttps://leetcode.com/problems/move-zeroes/)  
@ Tags: Array, Two Pointers     
@ Easy

------------------
## Solution
两个指针分别指向当前读写位置，若二者不一致时swap两个值。  
```java
class Solution {
    public void moveZeroes(int[] nums) {
        int read = 0, write = 0;
        while (read < nums.length) {
            if (nums[read] == 0) {
                read++;
                continue;
            }
            if (read != write) {
                nums[write] = nums[read];
                nums[read] = 0;
            }
            read++;
            write++;
        }
    }
}
```
