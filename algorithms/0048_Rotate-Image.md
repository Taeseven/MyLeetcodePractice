# Rotate Image
------------------
@ [Description](https://leetcode.com/problems/rotate-image/)  
@ Tags: Array    
@ Medium

------------------
## Solution
先将矩阵转置，再对每一行翻转处理。  
时间复杂度：$O(N^2)$  
空间复杂度：$O(1)$  
```java
class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;
//         transpose
        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                int tmp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = tmp;
            }
        }
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n / 2; j++) {
                int tmp = matrix[i][j];
                matrix[i][j] = matrix[i][n - j - 1];
                matrix[i][n - j - 1] = tmp;
            }
        }
    }
}
```
