#  Unique Paths III
------------------
@ [Description](https://leetcode.com/problems/minimum-path-sum/)  
@ Tags: DFS, Backtracking     
@ Medium

------------------
## Solution - DFS
DFS暴力解决，首先找到起点以及需要走的点的总个数。  
如果遇到终点，判断是否已经遍历了所有需要走的点，若是则返回1反之返回0。  
时间复杂度：$O(4^{MN})$  
空间复杂度：$O(MN)$  
```java
class Solution {
    public int uniquePathsIII(int[][] grid) {
        if (grid == null || grid.length == 0 || grid[0].length == 0)
            return 0;
        int m = grid.length, n = grid[0].length;
        int N = 0;
        int sx = -1, sy = -1;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] != -1)
                    N++;
                if (grid[i][j] == 1) {
                    sx = i;
                    sy = j;
                } 
            }
        }
        return dfs(grid, sx, sy, N-1);
    }
    private int dfs(int[][] grid, int x, int y, int N) {
        if (x < 0 || y < 0 || x >= grid.length || y >= grid[0].length || grid[x][y] == -1) return 0;
        if (grid[x][y] == 2)
            return (N==0)?1 : 0;
        grid[x][y] = -1;
        int count = dfs(grid, x+1, y, N-1) + dfs(grid, x-1, y , N - 1) + dfs(grid,x,y+1,N-1) + dfs(grid,x,y-1,N-1);
        grid[x][y] = 0;
        return count;
    }    
}
```
