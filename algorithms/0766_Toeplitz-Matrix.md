# Toeplitz Matrix
------------------
@ [Description](https://leetcode.com/problems/toeplitz-matrix/)  
@ Tags: Array     
@ Easy

------------------
## Solution
空间复杂度：$O(1)$  
时间复杂度：$O(MN)$  
```java
class Solution {
    public boolean isToeplitzMatrix(int[][] matrix) {
        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[0].length; j++) {
                if (i > 0 && j > 0 && matrix[i-1][j-1] != matrix[i][j])
                    return false;
            }
        }
        return true;
    }
}
```
