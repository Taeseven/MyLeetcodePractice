# Search Insert Position
------------------
@ [Description](https://leetcode.com/problems/search-insert-position/)  
@ Tags: Binary Search  
@ Easy

------------------
## Solution
因为是已经排序好的的数组，直接利用二分法查找即可。注意若数组不存在target也要返回其对应的插入位置。
```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int low = 0, high = nums.length - 1;
        while (low <= high) {
            int mid = (low + high) / 2;
            if (nums[mid] == target) return mid;
            else if (nums[mid] < target) low = mid + 1;
            else high = mid - 1; 
        }
        return low;
    }
}
```

