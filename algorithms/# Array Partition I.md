# Array Partition I
------------------
@ [Description](https://leetcode.com/problems/array-partition-i/)  
@ Tags: Array  
@ Easy

------------------
## Solution 1 - Sort
Sort后结果即为奇数index数字之和。  
```java
class Solution {
    public int arrayPairSum(int[] nums) {
        Arrays.sort(nums);
        int res = 0;
        for (int i = 0; i < nums.length; i+=2)
            res += nums[i];
        return res;
    }
}
```
