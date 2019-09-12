# Find First and Last Position of Element in Sorted Array
------------------
@ [Description](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)  
@ Tags: Array, Binary Search   
@ Medium

------------------
 # Solution - Binary Search
 利用二分法查找到与目标一致的数字，再对其两边进行寻找。  
 时间复杂度：$O(logN)$
 ```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int start = 0, end = nums.length - 1;
        int[] res = {-1, -1};
        while (start <= end) {
            int mid = (start + end)/2;
            if (nums[mid] == target) {
                return searchHelper(nums, res, mid);
            } else if (nums[mid] < target) start = mid + 1;
            else end = mid - 1;
        }
        return res;
    }
    
    private int[] searchHelper(int[] nums, int[] res, int mid) {
        if (nums.length == 1) {
            res[0] = res[1] = 0;
            return res;
        }
        int low = mid - 1, high = mid + 1;
        while (low >= 0 && nums[low] == nums[mid]) low--;
        while (high <= nums.length - 1 && nums[high] == nums[mid]) high++;
        if (low + 2 != high) {
            res[0] = low + 1;
            res[1] = high - 1;
        } else {
            res[0] = res[1] = mid;
        }
        return res;
    }
}
```
更好的解法：https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/solution/
