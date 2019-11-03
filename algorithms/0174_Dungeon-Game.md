# Dungeon Game
------------------
@ [Description](https://leetcode.com/problems/dungeon-game/)  
@ Tags: Binary Search, DP     
@ Hard

------------------
## Solution - DP
从右下角向左上角搜寻，将当前最小值填在array中。  
```java
class Solution {
    public int calculateMinimumHP(int[][] dungeon) {
        if (dungeon == null || dungeon.length == 0 || dungeon[0].length == 0)
            return 0;
        int m = dungeon.length, n = dungeon[0].length;
        int[][] hp = new int[m][n];
        hp[m-1][n-1] = Math.max(1, 1 - dungeon[m-1][n-1]);
        for (int i = m-2; i>= 0; i--)
            hp[i][n-1] = Math.max(1, hp[i+1][n-1] - dungeon[i][n-1]);
        for (int i = n-2; i>=0; i--)
            hp[m-1][i] = Math.max(1, hp[m-1][i+1] - dungeon[m-1][i]);
        for (int i = m-2; i >= 0; i--) {
            for (int j = n-2; j>= 0; j--) {
                int down = Math.max(1, hp[i+1][j] - dungeon[i][j]);
                int right = Math.max(1, hp[i][j+1] - dungeon[i][j]);
                hp[i][j] = Math.min(down, right);
            }
        }
        return hp[0][0];
    }
}
```
