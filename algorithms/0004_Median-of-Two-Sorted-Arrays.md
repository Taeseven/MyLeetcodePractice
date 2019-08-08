# Median of Two Sorted Arrays
------------------
@ [Description](https://leetcode.com/problems/median-of-two-sorted-arrays/)  
@ Tags: Arrays, Hash Table  
@ Hard

------------------

## Solution 1
可以直接按照大小顺序找到两个array的中位数。  
时间复杂度：$O(m+n)$  
```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int mid1 = 0, mid2 = 0;
        int index1 = 0, index2 = 0;
        for (int i = 0; i <= (nums1.length + nums2.length) / 2; i++) {
            mid1 = mid2;
            if (index1 == nums1.length) {
                mid2 = nums2[index2];
                index2++;
            }
            else if (index2 == nums2.length) {
                mid2 = nums1[index1];
                index1++;
            }
            else if (nums1[index1] <= nums2[index2]) {
                mid2 = nums1[index1];
                index1++;
            }
            else {
                mid2 = nums2[index2];
                index2++;
            }
        }
        if ((nums1.length + nums2.length) % 2 == 0) {
            return (mid1 + mid2) / 2.0;
        }
        return mid2;
    }
}
```

## Solution 2 - Binary Search
题目类似于找到两个有序数组中第k大的数。假设我们比较数组1的前$k/2$元素与数组2的前$k/2$元素，若$nums1[k/2] < num2[k/2]$则我们就要可以舍弃nums的前$k/2$个元素，依次类推得到结果。  
时间复杂度：$O(log(m+n))$  
空间复杂度：$O(1)$

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int total = nums1.length + nums2.length;
        if (total % 2 == 0) {
            return (medianHelper(nums1, 0, nums2, 0, total/2) + medianHelper(nums1, 0, nums2, 0, total/2 + 1)) / 2.0;
        }
        return medianHelper(nums1, 0, nums2, 0, total/2 + 1);
    }
    private int medianHelper(int[] nums1, int m, int[] nums2, int n, int k) {
        if (m >= nums1.length) return nums2[n + k - 1];
        if (n >= nums2.length) return nums1[m + k - 1];
        if (k == 1) return Math.min(nums1[m], nums2[n]);
        
        int a = m + k/2 - 1;
        int b = n + k/2 - 1;
        int mid1 = (a < nums1.length) ? nums1[a] : Integer.MAX_VALUE;
        int mid2 = (b < nums2.length) ? nums2[b] : Integer.MAX_VALUE;
        if (mid1 <= mid2) return medianHelper(nums1, m + k/2, nums2, n, k - k/2);
        return medianHelper(nums1, m, nums2, n + k/2, k - k/2);
    }
}
```