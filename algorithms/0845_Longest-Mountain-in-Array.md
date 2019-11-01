#  Longest Mountain in Array
------------------
@ [Description](https://leetcode.com/problems/longest-mountain-in-array/)  
@ Tags: Two Pointer     
@ Medium

------------------
## Solution
可以发现只有一个mountain结束时，下一个mountain才会开始。因此可以用两个指针遍历，当遍历完当前山脉后将start指针更新到end去。需要注意在array末尾可能出现只有上升区间的情况，或者start跳不出循环的情况，因此要用if判断以及max（end，start+1）解决。  
时间复杂度：$O(N)$  
空间复杂度：$O(1)$  
```java
class Solution {
    public int longestMountain(int[] A) {
        if (A == null || A.length < 3)
            return 0;
        int start = 0;
        int max = 0;
        while (start < A.length) {
            int end = start;
//             确保有上升区间
            if (end + 1 < A.length && A[end] < A[end + 1]) {
                while (end + 1 < A.length && A[end] < A[end + 1]) end++;
//                 确保有下降区间
                if (end + 1 < A.length && A[end] > A[end + 1]) {
                    while (end + 1 < A.length && A[end] > A[end + 1]) end++;
                    max = Math.max(max, end - start + 1);
                }
            }
//             处理指针在末尾时的情况
            start = Math.max(end, start + 1);
        }
        return max;
    }
}
```
