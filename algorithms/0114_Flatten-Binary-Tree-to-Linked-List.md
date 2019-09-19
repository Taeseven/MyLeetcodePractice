# Flatten Binary Tree to Linked List
@ [Description](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/)  
@ Tags: Tree, DFS        
@ Medium

------------------
## Solution 1
考虑到输出的为Linked List形式的树，left均为null。我们可以考虑先将右子树flatten，储存前一个node，将左子树移到右边后与prev进行连接即可。
```java
class Solution {
    private TreeNode prev = null;
    
    public void flatten(TreeNode root) {
        if (root == null) return;
        
        flatten(root.right);
        flatten(root.left);
        root.right = prev;
        root.left = null;
        prev = root;
    }
}
```
