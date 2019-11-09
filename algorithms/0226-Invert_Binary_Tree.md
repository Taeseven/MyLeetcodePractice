# Invert Binary Tree
------------------
@ [Description](https://leetcode.com/problems/invert-binary-tree/)  
@ Tags: Tree    
@ Easy

------------------
## Solution 1 - Recursive
```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null)
            return root;
        TreeNode left = invertTree(root.right);
        TreeNode right = invertTree(root.left);
        root.left = left;
        root.right = right;
        return root;
    }
}
```

## Solution 2 - Iterative
```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null)
            return root;
        Queue<TreeNode> que = new LinkedList<>();
        que.offer(root);
        while (!que.isEmpty()) {
            int len = que.size();
            for (int i = 0; i < len; i++) {
                TreeNode curr = que.poll();
                TreeNode tmp = curr.left;
                curr.left = curr.right;
                curr.right = tmp;
                if (curr.left != null) que.offer(curr.left);
                if (curr.right != null) que.offer(curr.right);
            }
        }
        return root;
    }
}
```
