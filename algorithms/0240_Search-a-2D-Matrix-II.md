#  Search a 2D Matrix II
------------------
@ [Description](https://leetcode.com/problems/search-a-2d-matrix-ii/)  
@ Tags: Binary Search, Dive and Conquer     
@ Medium

------------------
## Solution 1 - Binary Search
可以以对角线为基准，因为对角线上的元素从上到下单调递增。遍历对角线，分别对以对角线为基准进行二分查找。  
时间复杂度：$O(log(N!))$  

## Solution 2 - Dive and Conquer
可以针对每一个位置将其分为4个排序好的子矩阵，其中两个为寻找空间。  
时间复杂度：$O(NlogN)$  

## Solution 3 - Reduce Search Space
从右上角或左下角出发进行寻找，类似于走台阶。  
时间复杂度：$O(m+n)$
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0)
            return false;
        int row = 0;
        int col = matrix[0].length - 1;
        while (row < matrix.length && col >= 0) {
            if (matrix[row][col] == target)
                return true;
            else if (matrix[row][col] > target)
                col--;
            else
                row++;
        }
        return false;
    }
}
```
