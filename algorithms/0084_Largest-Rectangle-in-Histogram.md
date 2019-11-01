# Largest Rectangle in Histogram
------------------
@ [Description](https://leetcode.com/problems/largest-rectangle-in-histogram/)  
@ Tags: Array, Stack     
@ Hard

------------------
## Solution 1 - Brute Force
时间复杂度：$O(N^2)$  
空间复杂度：$O(1)$  
```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        int max = 0;
        for (int i = 0; i <heights.length; i++) {
            int height = Integer.MAX_VALUE;
            for (int j = i; j < heights.length; j++) {
                height = Math.min(height, heights[j]);
                max = Math.max(max, height * (j-i+1));
            }
        }
        return max;
    }
}
```

## Solution 2 - Stack
用stack维护一个单调递增的栈:  
其意义在于当出现的新长度小于栈顶的长度时，意味着以前一个长度为高的矩形的终止，因此可以将其pop出去并计算该值，该矩形的宽就是当前index减去pop后peek的index再减去1。栈先进-1是为了方便处理栈为空的情况。  
时间和空间复杂度都是$O(N)$  
```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        Stack<Integer> stack = new Stack<>();
        stack.push(-1);
        int max = 0;
        for (int i = 0; i < heights.length; i++) {
            while (stack.peek() != -1 && heights[stack.peek()] >= heights[i])
                max = Math.max(max, heights[stack.pop()] * (i - stack.peek() - 1));
            stack.push(i);
        }
        while (stack.peek() != -1) {
            max = Math.max(max, heights[stack.pop()] * (heights.length - stack.peek() -1));
        }
        return max;
        
    }
}
```
## Solution 3 - Divid and Conquer
找到区间内最小的height，那么它所能·构成的最大矩形是区间长度乘以最小的高度。如果有比它更大的矩形，那么一定在最小高度的两边，因此可以找到最小高度然后用分治法解决问题，直到区间的长度为一停止。  
时间复杂度最优为$O(NlogN)，最差是若是sort的矩阵则为$O(N^2)$  
空间复杂度为$O(N)$  
```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        return helper(heights,0,heights.length-1);
    }
    private int helper(int[] heights, int start, int end) {
        if (start > end)
            return 0;
        int min = start;
        for (int i = start; i <= end; i++) {
            min = (heights[min] > heights[i]) ? i : min;
        }
        return Math.max(heights[min]*(end-start+1), Math.max(helper(heights,min+1,end), helper(heights,start,min-1)));
    }
}
```
