#  Clone Graph
------------------
@ [Description](https://leetcode.com/problems/clone-graph/)  
@ Tags: DFS, BFS   
@ Medium

------------------
## Solution 1 - DFS
时间复杂度：$O(N)$  
空间复杂度：$O(N)$  
```java
class Solution {
    HashMap<Node, Node> map = new HashMap<>();
    public Node cloneGraph(Node node) {
        if (node.neighbors.size() == 0)
            return new Node(node.val, new ArrayList<>());
        dfs(node);
        for (Node key : map.keySet()) {
            Node tmp = map.get(key);
            for (Node neighbor : key.neighbors) {
                tmp.neighbors.add(map.get(neighbor));
            }
        }
        return map.get(node);
    }
    private void dfs(Node node) {
        for (Node n : node.neighbors) {
            if (!map.containsKey(n)) {
                Node tmp = new Node(n.val, new ArrayList<>());
                map.put(n, tmp);
                dfs(n);
            }
        }
    }
}
```

## Solution 2 - BFS
```java
class Solution {
    public Node cloneGraph(Node node) {
        if (node.neighbors.size() == 0)
            return new Node(node.val, new ArrayList<>());
        HashMap<Node, Node> map = new HashMap<>();
        Queue<Node> queue = new LinkedList<>();
        queue.offer(node);
        map.put(node, new Node(node.val, new ArrayList<>()));
        
        while (!queue.isEmpty()) {
            Node tmp = queue.poll();
            for (Node neighbor : tmp.neighbors) {
                if (!map.containsKey(neighbor)) {
                    map.put(neighbor, new Node(neighbor.val, new ArrayList<>()));
                    queue.offer(neighbor);
                }
                map.get(tmp).neighbors.add(map.get(neighbor));
            }
        }      
        return map.get(node);
    }
}
```

