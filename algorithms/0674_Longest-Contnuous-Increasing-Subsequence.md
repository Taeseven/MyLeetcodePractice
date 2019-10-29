# Longest Continuous Increasing Subsequence
------------------
@ [Description](https://leetcode.com/problems/longest-continuous-increasing-subsequence/)  
@ Tags: Array     
@ Easy

------------------
## Solution
```java
// version 1
class Solution {
    public int findLengthOfLCIS(int[] nums) {
        if (nums == null || nums.length == 0)
            return 0;
        int res = 0;
        int left = 0;
        for (int i = 0; i < nums.length; i++) {
            if (i > 0 && nums[i] <= nums[i - 1]) {
                left = i;
            }
            res = Math.max(res, i - left + 1);
        }
        return res;
    }
}

// version 2
class Solution {
    public int findLengthOfLCIS(int[] nums) {
        if (nums == null || nums.length == 0)
            return 0;
        int res = 1;
        int curr = 1;
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] > nums[i - 1]) {
                curr++;
                res = (curr > res) ? curr : res;
            } else {
                curr = 1;
            }
        }
        return res;
    }
}
```

## Follow Up 1
允许有一个break，允许有一个下降或者相等。  
例如[1,2,3,0,1,-4]即输出5.  
```java
class Solution {
    public int findLengthOfLCIS(int[] nums) {
        if (nums == null || nums.length == 0)
            return 0;
        int res = 0;
        int left = 0;
        int break_point = 0;
        for (int i = 0; i < nums.length; i++) {
            if (i > 0 && nums[i] <= nums[i - 1]) {
                if (break_point > left) {
                    left = break_point; 
                }
                break_point = i;
            }
            res = Math.max(res, i - left + 1);
        }
        return res;
    }
}
```
记录break_point的位置即可，判断其与left的关系即可。  

## Follow Up 2
如果允许k个break呢？  
可以考虑sliding window，时间复杂度为$O(N^2)$  
或者考虑所有记录break_point的位置，不断的pop出最小的点，但是会牺牲空间。  
