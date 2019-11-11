# Squares of a Sorted Array
------------------
@ [Description](https://leetcode.com/problems/squares-of-a-sorted-array/)  
@ Tags: Array, Two Pointers    
@ Easy

------------------
## Solution 1 - Sort
平方后sort。  
时间复杂度：$O(NlogN)$  
空间复杂度：$O(N)$  

## Solution 2 - Two Pointers
找到符号变化的位置，比较两指针即可。  
时间复杂度：$O(N)$  
空间复杂度：$O(N)$  
```java
class Solution {
    public int[] sortedSquares(int[] A) {
        if (A == null || A.length == 0)
            return A;
        int[] res = new int[A.length];
        int right = 0;
        while (right < A.length && A[right] < 0) right++;
        int left = right - 1;
        int index = 0;
        while (left >= 0 && right < A.length) {
            if (-A[left] > A[right]) {
                res[index++] = A[right] * A[right];
                right++;
            } else {
                res[index++] = A[left] * A[left];
                left--;
            }
        }
        while (left >= 0) {
            res[index++] = A[left] * A[left];
            left--;
        }
        while (right < A.length) {
            res[index++] = A[right] * A[right];
            right++;
        }
        return res;
    }
}
```
