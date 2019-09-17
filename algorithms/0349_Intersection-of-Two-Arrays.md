# Intersection of Two Arrays
@ [Description](https://leetcode.com/problems/intersection-of-two-arrays/)  
@ Tags: Hash Table, Two Pointers, Binary Search, Sort    
@ Easy

------------------
## Solution 1 - Hash Table
用两个HashSet取交集。
```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        HashSet<Integer> set = new HashSet<Integer>();
        HashSet<Integer> set_tmp = new HashSet<Integer>();
        for (Integer num : nums1) set.add(num);
        for (Integer num : nums2) {
            if (set.contains(num) && !set_tmp.contains(num))
                set_tmp.add(num);
        }
        int[] res = new int[set_tmp.size()];
        int idx = 0;
        for (int nums : set_tmp) res[idx++] = nums;
        return res;
    }
}
```
