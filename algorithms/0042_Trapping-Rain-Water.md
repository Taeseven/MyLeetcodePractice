# Trapping Rain Water
------------------
@ [Description](https://leetcode.com/problems/trapping-rain-water/)  
@ Tags: Array, Two Pointers, Stack  
@ Hard

------------------
## Solution - Two Pointers
记录左右边界，并对其不断更新。  
左右分别两个指针，仅对较小值的指针进行移位。（较大值和另一边的边界可以包含较小值指针）  
时间复杂度$O(n)$  
空间复杂度$O(1)$  
```java
class Solution {
    public int trap(int[] height) {
        // edge case
        if (height.length <= 2) {
            return 0;
        }
        int res = 0;
        int left = 0, right = height.length - 1;
        int left_max = 0, right_max = 0;
        while (left <= right) {
            if (height[right] > height[left]) {
                if (height[left] > left_max) {
                    left_max = height[left];
                } else {
                    res += left_max - height[left];
                    left++;
                } 
            } else {
                if (height[right] > right_max) {
                    right_max = height[right];
                } else {
                    res += right_max - height[right];
                }
                right--; 
            }
        }
        return res;
    }
}
```

## Solution 2 - Stack
让stack保持单调递减的状态，若出现当前值大于栈顶时则代表其可以存在空间。  
时间空间复杂度均为$O(n)$  
```java
class Solution {
    public int trap(int[] height) {
        if (height.length <= 2) {
            return 0;
        }
        
        int res = 0, curr = 0;
        Stack<Integer> stack = new Stack<>();
        
        while (curr < height.length) {
            while (!stack.isEmpty() && height[curr] >= height[stack.peek()]) {
                int peek = stack.pop();
                if (stack.isEmpty()) {
                    break;
                }
                res += (curr - stack.peek() - 1) * (Math.min(height[curr], height[stack.peek()]) - height[peek]);
            }   
            stack.push(curr++);
        }
        return res;
    }
}
```

## Solution 3 - DP
pre-compute从左/右开始到当前位置的最大值，即为边界。两个边界的最小值与当前值的差即为可容纳的体积，若小于0舍去即可。  
空间时间复杂度均为$O(n)$  
```java
class Solution {
    public int trap(int[] height) {
        if (height.length <= 2) {
            return 0;
        }
        
        int n = height.length;
        int[] left = new int[n];
        int[] right = new int[n];
        left[0] = height[0];
        right[n - 1] = height[n - 1];
        for (int i = 1, j = n - 2; i < n; i++, j--) {
            left[i] = Math.max(left[i - 1], height[i]);
            right[j] = Math.max(right[j + 1], height[j]);
        }
        
        int res = 0;
        for (int i = 1; i < n - 1; i++) {
            int tmp = Math.min(left[i - 1], right[i + 1]) - height[i];
            res += tmp > 0 ? tmp : 0;
        }
        return res;
    }
}
```
