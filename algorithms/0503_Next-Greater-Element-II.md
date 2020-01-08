# Next Greater Element II
------------------
@ [Description](https://leetcode.com/problems/next-greater-element-ii/)  
@ Tags: Stack   
@ Medium

------------------
 # Solution
遍历两边，用stack维持递减的序列。若新元素大于栈顶则pop，注意要处理index。  
时间复杂度：$O(N)$  
空间复杂度：$O(N)$
```java
class Solution {
    public int[] nextGreaterElements(int[] nums) {
        int[] res = new int[nums.length];
        Arrays.fill(res, -1);
        Stack<Integer> stack = new Stack<>();
        for (int i = 0; i < 2 * nums.length - 1; i++) {
            while (!stack.isEmpty() && nums[stack.peek() % nums.length] < nums[i % nums.length]) {
                res[stack.pop() % nums.length] = nums[i % nums.length];
            }
            stack.push(i);
        }
        return res;
    }
}
```
