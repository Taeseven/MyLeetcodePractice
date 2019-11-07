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

## Solution 2 - Two Pointers
sort，然后利用两个指针处理。
```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        if (nums1 == null || nums1.length == 0 || nums2 == null || nums2.length == 0)
            return new int[0];
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        Set<Integer> set = new HashSet<>();
        int i = 0, j = 0;
        while (i < nums1.length && j < nums2.length) {
            if (nums1[i] == nums2[j]) {
                set.add(nums1[i]);
                i++; j++;
            } else if (nums1[i] < nums2[j]) i++;
            else j++;
        }
        int[] res = new int[set.size()];
        i = 0;
        for (Integer n : set)
            res[i++] = n;
        return res;
    }
}
```
