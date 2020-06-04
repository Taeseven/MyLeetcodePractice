# Minimum Cost Tree From Leaf Values
------------------
@ [Description](https://leetcode.com/problems/minimum-cost-tree-from-leaf-values/)  
@ Tags: DP, Stack, Tree   
@ Medium

------------------
## Solution 1 - DP
首先构造出任意两index间的最大value，然后根据arr长度不断增加遍历整个array。  
时间复杂度：$O(n^3)$  
空间复杂度：$O(n^2)$  
```java
class Solution {
    public int mctFromLeafValues(int[] arr) {
        int len = arr.length;
        
        // max[i][j] represents the max value in arr[i:j]
        int[][] max = new int[len][len];
        // dp[i][j] represents the min cost in arr[i:j]
        int[][] dp = new int[len][len];
        
        // construct max
        for (int i = 0; i < len; i++) {
            max[i][i] = arr[i];
            for (int j = i + 1; j < len; j++) {
                max[i][j] = Math.max(max[i][j - 1], arr[j]);
            }
        }
        
        // dp
        // important: the main loop should be lenth
        // otherwise some item in dp may not be updated yet
        for (int l = 1; l < len; l++) {
            for (int i = 0; i + l < len; i++) {
                int j = i + l;
                dp[i][j] = Integer.MAX_VALUE;
                // search where to split into subtrees
                for (int k = i; k < j; k++) {
                    dp[i][j] = Math.min(dp[i][j],
                                        dp[i][k] + dp[k + 1][j] + max[i][k] * max[k + 1][j]);
                }
            }
        }

        return dp[0][len - 1];
    }
}
```

## Solution 2 - Stack
较大值的深度尽可能小。当前值大于栈顶值时，意味着出现了转折点，我们需要判断到底归属于左右哪一侧。当遍历完成时，栈保持单调递减的状态，那么栈顶元素相应成对，不断推出栈即可。  
有点类似栈中元素是各枝中的最大数值，尽可能将较小的各枝放在一起。  
[视频讲解](https://www.youtube.com/watch?v=xcYkzSrgOmY)  
时间和空间复杂度均为$O(n)$  
```java
class Solution {
    public int mctFromLeafValues(int[] arr) {
        Stack<Integer> stack = new Stack();
        int cost = 0;
        
        // avoid empty stack
        stack.push(Integer.MAX_VALUE);
        for (int num : arr) {
            while (stack.peek() <= num) {
                int tmp = stack.pop();
                cost += tmp * Math.min(stack.peek(), num);
            }
            stack.push(num);
        }
        
        // stack[0] is the MAX_VALUE bound
        while (stack.size() > 2) {
            cost += stack.pop() * stack.peek();
        }
        
        return cost;
    }
}
```
