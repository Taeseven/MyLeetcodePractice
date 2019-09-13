# Search a 2D Matrix
@ [Description](https://leetcode.com/problems/search-a-2d-matrix/)  
@ Tags: Array, Binary Search  
@ Medium

------------------
## Solution - Binary Search
考虑将matrix展成长array即可，与正常的二分法一致。  
注意考虑特殊情况，矩阵横向或竖向为空。
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix.length == 0 || matrix[0].length == 0)
            return false;
        int min = 0, max = matrix.length * matrix[0].length - 1;
        while (min + 1 < max) {
            int mid = min + (max - min) / 2;
            int tmp = matrix[mid/matrix[0].length][mid%matrix[0].length];
            if (tmp == target)
                return true;
            else {
                if (tmp > target)
                    max = mid;
                else
                    min = mid;
            }
        }
        if (matrix[min/matrix[0].length][min%matrix[0].length] == target || matrix[max/matrix[0].length][max%matrix[0].length] == target)
            return true;
        else
            return false;
    }
}
```
