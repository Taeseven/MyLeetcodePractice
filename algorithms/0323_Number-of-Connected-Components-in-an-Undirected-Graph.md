#  Number of Connected Components in an Undirected Graph
------------------
@ [Description](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/)  
@ Tags: DFS, BFS, Union Find, Graph     
@ Medium

------------------
## Solution - Union Find
时间复杂度：$N\alpha$  
空间复杂度：$O(N)$
```java
class Solution {
    public int countComponents(int n, int[][] edges) {
        int[] roots = new int[n];
        for (int i = 0; i < n; i++) 
            roots[i] = i;
        int res = n;
        for (int[] edge : edges) {
            int root1 = find(roots, edge[0]);
            int root2 = find(roots, edge[1]);
            if (root1 != root2) {
                roots[root1] = root2;
                res--;
            }
        }
        return res;
    }
    private int find(int[] roots, int val) {
        if (roots[val] == val)
            return val;
        roots[val] = roots[roots[val]];
        return find(roots, roots[val]);
    }
}
```
