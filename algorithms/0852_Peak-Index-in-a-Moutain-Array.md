# Peak Index in a Mountain Array
@ [Description](https://leetcode.com/problems/peak-index-in-a-mountain-array/)  
@ Tags: Array, Binary Search  
@ Easy

------------------
## Solution
改变二分法判断条件即可
```java
class Solution {
    public int peakIndexInMountainArray(int[] A) {
        int left = 0, right = A.length - 1;
        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (A[mid] > A[mid - 1] && A[mid] > A[mid + 1])
                return mid;
            else {
                if (A[mid] < A[mid + 1])
                    left = mid;
                else
                    right = mid;
            }
        }
        return (A[right] > A[left]) ? right : left;
    }
}
```
