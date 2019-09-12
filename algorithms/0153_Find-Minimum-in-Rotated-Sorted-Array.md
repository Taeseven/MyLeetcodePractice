# Find Minimum in Rotated Sorted Array
------------------
@ [Description](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)  
@ Tags: Array, Binary Search   
@ Medium

------------------
# Solution
其实等同于寻找first position < last number  
```java
class Solution {
    public int findMin(int[] nums) {
        if (nums.length == 1) {
            return nums[0];
        }
        int left = 0, right = nums.length - 1;
        int target = nums[right];
        if (nums[0] < nums[right]) {
            return nums[0];
        }
        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] >= target) {
                left = mid;
            } else {
                right = mid;
            }
        }
        return Math.min(nums[left], nums[right]);
    }
}
```
当然也可以寻找改变上升趋势的位置。

