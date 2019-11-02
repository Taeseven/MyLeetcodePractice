# Next Greater Element I
------------------
@ [Description](https://leetcode.com/problems/next-greater-element-i/)  
@ Tags: Stack     
@ Easy

------------------
## Solution
先遍历较长的array，寻找每个元素的下一个大于他的元素，可以利用stack以及访问过但尚未找到比它大的元素的元素。  
时间复杂度：$O(M+N)$  
空间复杂度：$O(N)$  
```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        Stack<Integer> stack = new Stack<>();
        Map<Integer, Integer> map = new HashMap<>();
        int[] res = new int[nums1.length];
        for (int i = 0; i < nums2.length; i++) {
            while (!stack.isEmpty() && nums2[i] > stack.peek())
                map.put(stack.pop(), nums2[i]);
            stack.push(nums2[i]);
        }
        while (!stack.isEmpty())
            map.put(stack.pop(), -1);
        for (int i = 0; i < nums1.length; i++) 
            res[i] = map.get(nums1[i]);
        return res;
    }
}
```
