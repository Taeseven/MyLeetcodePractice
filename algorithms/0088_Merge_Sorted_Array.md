#  Merge Sorted Array
------------------
@ [Description](https://leetcode.com/problems/merge-sorted-array/)  
@ Tags: Array, Two Pointer    
@ Easy

------------------
## Solution
从末尾开始排序可以达到in-place
```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        m = m - 1;
        n = n - 1;
        int idx = m + n - 1;
        while (m >= 0 && n >= 0) {
            nums1[idx--] = (nums1[m] > nums2[n]) ? nums1[i--] : nums2[j--];
        }
        while (j >= 0) {
            nums1[idx--] = nums2[j--];
        }
    }
}
```
