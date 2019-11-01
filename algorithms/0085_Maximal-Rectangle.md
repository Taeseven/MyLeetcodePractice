# Maximal Rectangle
------------------
@ [Description](https://leetcode.com/problems/maximal-rectangle/)  
@ Tags: Array, Stack, HashTable, DP     
@ Hard

------------------
## Solution 1 - Stack + DP
可以联系到Leetcode 84，以每行为底将其转变为hist进行计算。  
时间复杂度：$O(MN)$  
空间复杂度：$O(N)$  
```java
class Solution {
    public int maximalRectangle(char[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0)
            return 0;
        int[] hist = new int[matrix[0].length];
        int max = 0;
        for (int i = 0; i < matrix.length; i++) {
//             get histogram for each row;
            for (int j = 0; j < matrix[0].length; j++) {
                hist[j] = (matrix[i][j] == '1') ? hist[j] + 1 : 0;
            }
            max = Math.max(max, getMax(hist));
        }
        return max;
    }
    
    private int getMax(int[] hist) {
        Stack<Integer> stack = new Stack<>();
        stack.push(-1);
        int max = 0;
        for (int i = 0; i < hist.length; i++) {
            while (stack.peek() != -1 && hist[stack.peek()] >= hist[i])
                max = Math.max(max, hist[stack.pop()] * (i - stack.peek() - 1));
            stack.push(i);
        }
        while (stack.peek() != -1)
            max= Math.max(max, hist[stack.pop()] * (hist.length - stack.peek() - 1));
        return max;
        
    }
}
```

## Solution 2 - DP


