# Search in Rotated Sorted Array
------------------
@ [Description](https://leetcode.com/problems/search-in-rotated-sorted-array/)  
@ Tags: Array, Binary Search   
@ Medium

------------------
 # Solution
虽然进行了旋转，但是旋转的两个部分以后遵循着sorted的规则，因此可以用二分法对进行寻找，根据不同情况进行分析。
```java
class Solution {
    public int search(int[] nums, int target) {
        int start = 0, end = nums.length - 1;
        while (start <= end) {
            int mid = (start + end)/2;
            if (target == nums[mid]) return mid;
            if (nums[start] <= nums[mid]) {
                if (target >= nums[start] && target <= nums[mid])
                    end = mid - 1;
                else start = mid + 1;
            } else {
                if (target <= nums[end] && target >= nums[mid]) start = mid + 1;
                else end = mid - 1;
            }
            
        }
        return -1;
    }
}
```
