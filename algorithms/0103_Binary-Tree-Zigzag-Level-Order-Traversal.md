# Binary Tree Zigzag Level Order Traversal
------------------
@ [Description](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/)  
@ Tags: Tree, BFS   
@ Medium

------------------
## Solution
与Leetcode 102一样,需要用LinkedList实现每个level变换数字顺序。  
```java
class Solution {
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) return res;
        Queue<TreeNode> que = new LinkedList<>();
        int level = 0;
        que.offer(root);
        while (!que.isEmpty()) {
            LinkedList<Integer> tmp = new LinkedList<>();
            int size = que.size();
            for (int i = 0; i < size; i++) {
                TreeNode node = que.poll();
                if (level % 2 == 0) tmp.addLast(node.val);
                else tmp.addFirst(node.val);
                if (node.left != null) que.offer(node.left);
                if (node.right != null) que.offer(node.right);
            }
            res.add(tmp);
            level += 1;
        }
        return res;
    }
}
```
