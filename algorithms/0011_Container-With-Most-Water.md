# Container With Most Water
---------------
@[Description](https://leetcode.com/problems/container-with-most-water/)  
@ Medium
---------------
## Solution 1 - Brute Force
时间复杂度：$O(n^2)$
空间复杂度：$O(1)$

## Solution 2 - Two Pointer
首尾各放一个指针，根据首尾的数值将数值较小的指针向中间移动，在遍历过程中记录面积最大值即可。  
时间复杂度：$O(n)$
空间复杂度：$O(1)$

```java
class Solution {
    public int maxArea(int[] height) {
        int left = 0, right = height.length - 1;
        int s = 0, h = 0;
        while (left < right) {
            h = Math.min(height[left], height[right]);
            s = Math.max(s, h * (right - left));
            if (height[left] <= h) left++;
            else right--;
        }
        return s;
    }
}
```
