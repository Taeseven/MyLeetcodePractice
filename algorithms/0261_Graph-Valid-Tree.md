# Graph Valid Tree
------------------
@ [Description](https://leetcode.com/problems/graph-valid-tree/)  
@ Tags: Graph, DFS, BFS, Union Find   
@ Medium

------------------
## Solution 1 - BFS
首先若为树的话，必有n-1条边。  
然后再判断从一个node是否可以访问到其他所有的node。  
考虑用BFS来解题，首先需要将edges重写成graph的格式，然后看是否可以访问到每个node。要注意由于是无向图，需要一个Set去存所有已经访问过的节点。  
时间复杂度和空间复杂度均为：$O(E)$ （E为edges的个数）  
```java
class Solution {
    public boolean validTree(int n, int[][] edges) {
        if (edges.length != n - 1) return false;
        
        Map<Integer, Set<Integer>> graph = getGraph(n, edges);
        
        Queue<Integer> queue = new LinkedList<>();
        Set<Integer> set = new HashSet<>();
        
        queue.offer(0);
        set.add(0);
        int count = 0;
        while (!queue.isEmpty()) {
            int node = queue.poll();
            count++;
            for (Integer neighbor : graph.get(node)) {
                if (set.contains(neighbor))
                    continue;
                set.add(neighbor);
                queue.offer(neighbor);
            }
        }
        return count == n;
        
    }
    
    private Map<Integer, Set<Integer>> getGraph(int n, int[][] edges) {
        Map<Integer, Set<Integer>> graph = new HashMap<>();
        for (int i = 0; i < n; i++) {
            graph.put(i, new HashSet<Integer>());
        }
        for (int[] edge : edges) {
            int i = edge[0];
            int j = edge[1];
            graph.get(i).add(j);
            graph.get(j).add(i);
        }
        return graph;
    }
}
```

## Solution 2 - Union Find
若为树，则每条边都会将不属于同一set的两个节点连接起来。因此只需要判断两节点是否属于同一set即可。  
空间复杂度：$O(V)$  
时间复杂度：$O(VE)$  
```java
class Solution {
    public boolean validTree(int n, int[][] edges) {
        if (edges.length != n - 1) return false;
        
        int[] nodes = new int[n];
        Arrays.fill(nodes, -1);
        
        for (int i = 0; i< n - 1; i++) {
            int x = find(nodes, edges[i][0]);
            int y = find(nodes, edges[i][1]);
            if (x == y)
                return false;
            nodes[x] = y;
        }
        return true;
    }
    
    private int find(int[] nodes, int i) {
        if (nodes[i] == -1)
            return i;
        return find(nodes, nodes[i]);
    }
}
```
