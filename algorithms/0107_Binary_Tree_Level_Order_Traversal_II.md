# Binary Tree Level Order Traversal II
------------------
@ [Description](https://leetcode.com/problems/binary-tree-level-order-traversal-ii/)  
@ Tags: Tree, BFS   
@ Medium

------------------
## Solution
与Leetcode 102一样，这里只需要利用LinkedList进行addFirst操作即可。或者使用ArrayList使用list.add(0, tmp).  
```java
class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        LinkedList<List<Integer>> res = new LinkedList<>();
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
            res.addFirst(tmp);
        }
        return res;
    }
}
```
