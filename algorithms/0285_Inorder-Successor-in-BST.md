# Binary Search Tree Iterator
------------------
@ [Description](https://leetcode.com/problems/binary-search-tree-iterator/)  
@ Tags: Tree  
@ Medium

------------------
## Solution
时间复杂度：$O(h)$  
空间复杂度：$O(1)$  
```java
class Solution {
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        if (root == null)
            return null;
        if (root.val <= p.val)
            return inorderSuccessor(root.right, p);
        else {
            TreeNode tmp = inorderSuccessor(root.left, p);
            return (tmp != null) ? tmp : root;
        }
    }
}
```
