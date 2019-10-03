# Binary Tree Level Order Traversal
------------------
@ [Description](https://leetcode.com/problems/binary-tree-level-order-traversal/)  
@ Tags: Tree, BFS   
@ Medium

------------------
## Solution
用一个Queue去记录各个level的节点，注意因为Queue的size是变化的，一定在遍历的过程前先取出size。  
queue.add()和queue.remove()会抛出异常，而queue.offer()和queue.poll()则不会。  
时间复杂度和空间负责度均为：$O(N)$  
```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) return res;
        Queue<TreeNode> que = new LinkedList<>();
        que.offer(root);
        while (!que.isEmpty()) {
            List<Integer> tmp = new ArrayList<>();
            int size = que.size();
            for (int i = 0; i < size; i++) {
                TreeNode node = que.poll();
                tmp.add(node.val);
                if (node.left != null) que.offer(node.left);
                if (node.right != null) que.offer(node.right);
            }
            res.add(tmp);
        }
        return res;
    }
}
```
