#  Two Sum Less Than K
------------------
@ [Description](https://leetcode.com/problems/two-sum-less-than-k//)  
@ Tags: Two Pointer, Array    
@ Easy

------------------
## Solution
时间复杂度：$O(N)+O(NlogN)$  
空间复杂度：$O(1)$  
```java
class Solution {
    public int twoSumLessThanK(int[] A, int K) {
        if (A == null || A.length < 2)
            return -1;
        Arrays.sort(A);
        int left = 0, right = A.length - 1;
        int res = 0, max = 0;
        while (left < right) {
            if (A[left] + A[right] < K) {
                res += right - left;
                max = Math.max(max, A[left] + A[right]);
                left++;
            } else {
                right--;
            }
        }
        return (res == 0) ? -1 : max;
    }
}
```
