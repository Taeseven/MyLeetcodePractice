# Check If a Number Is Majority Element in a Sorted Array
------------------
@ [Description](https://leetcode.com/problems/check-if-a-number-is-majority-element-in-a-sorted-array/)  
@ Tags: Array, Binary Search  
@ Easy

------------------
## Solution
寻找第一次出现target的位置，判断在其后len/2的位置是否还等于target即可。code based on 九章的模板（可以避免死循环，但需要double check）  
时间复杂度：$O(logN)$
```java
class Solution {
    public boolean isMajorityElement(int[] nums, int target) {
        int idx = firstPosition(nums, target);
        if (idx == -1 || idx + nums.length/2 > nums.length - 1) {
            return false;
        }
        if (nums[idx + nums.length/2] == target) {
            return true;
        }
        return false;
        
    }
    
    private int firstPosition(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                right = mid;
            } else if (nums[mid] > target) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
        if (nums[left] == target) {
            return left;
        }
        if (nums[right] == target) {
            return right;
        }
        return -1;
    }
}
```
