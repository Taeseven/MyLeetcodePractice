#  Spiral Matrix
------------------
@ [Description](https://leetcode.com/problems/spiral-matrix/)  
@ Tags: Array     
@ Medium

------------------
## Solution
时间空间复杂度均为$O(N)$  
```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> res = new LinkedList<>();
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0)
            return res;
        int rowBegin = 0, colBegin = 0;
        int rowEnd = matrix.length - 1, colEnd = matrix[0].length - 1;
        while (rowBegin <= rowEnd && colBegin <= colEnd) {
            for (int i = colBegin; i <= colEnd; i++)
                res.add(matrix[rowBegin][i]);
            for (int i = rowBegin + 1; i <= rowEnd; i++)
                res.add(matrix[i][colEnd]);
            if (rowBegin == rowEnd || colBegin == colEnd)
                break;
            for (int i = colEnd - 1; i >= colBegin; i--)
                res.add(matrix[rowEnd][i]);
            for (int i = rowEnd - 1; i > rowBegin; i--)
                res.add(matrix[i][colBegin]);
            rowBegin++;
            rowEnd--;
            colBegin++;
            colEnd--;
        }
        return res;
    }
}
```
