# Find Peak Element
@ [Description](https://leetcode.com/problems/find-peak-element/)  
@ Tags: Array, Binary Search  
@ Medium

------------------
## Solution
```java
class Solution {
    public int findPeakElement(int[] nums) {
        int left = 0, right = nums.length - 1;
        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] > nums[mid - 1] && nums[mid] > nums[mid + 1])
                return mid;
            else {
                if (nums[mid] < nums[mid + 1])
                    left = mid;
                else
                    right = mid;
            }
        }
        return (nums[right] > nums[left]) ? right : left;
    }
}
```
