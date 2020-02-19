# Number of Islands II
------------------
@ [Description](https://leetcode.com/problems/number-of-islands-ii/)  
@ Tags: Union Find    
@ Hard

------------------
## Solution
利用Union Find存储每个点的root，每次添加新的island时只有检查四个方向的点是否为island；如果True，则需要查找两点的root如果相同则不需进行任何操作，反之将两个set union并减少count。  
时间复杂度：$O(k)$  
空间复杂度：$O(mn)$  
```java
class Solution {
    public List<Integer> numIslands2(int m, int n, int[][] positions) {
        int[] root = new int[m * n + 1];
        int count = 0;
        List<Integer> res = new ArrayList<>();
        for (int[] pos : positions) {
            int x = pos[0];
            int y = pos[1];
            int idx = x * n + y + 1;
            if (root[idx] == 0) {
                root[idx] = idx;
                count++;
            }
            if (x > 0 && root[idx - n] != 0) {
                count = union(root, idx, idx - n, count);
            }
            if (x < m - 1 && root[idx + n] != 0) {
                count = union(root, idx, idx + n, count);
            }
            if (y > 0 && root[idx - 1] != 0) {
                count = union(root, idx, idx - 1, count);
            }
            if (y < n - 1 && root[idx + 1] != 0) {
                count = union(root, idx, idx + 1, count);
            }
            res.add(count);
        }
        return res;
    }
    
    private int find(int[] root, int x) {
        if (root[x] == x)
            return x;
        root[x] = find(root, root[x]);
        return root[x];
    }
    
    private int union(int[] root, int x, int y, int count) {
        int x_root = find(root, x);
        int y_root = find(root, y);
        if (x_root != y_root) {
            root[x_root] = y_root;
            count--;
        }
        return count;
    }
}
```
