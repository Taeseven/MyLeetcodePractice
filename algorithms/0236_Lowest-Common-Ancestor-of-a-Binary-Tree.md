# Lowest Common Ancestor of a Binary Tree
@ [Description](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)  
@ Tags: Tree        
@ Medium

------------------
## Solution 1
分治法。判断左右子树是否存在两个要找的值，遇到要找的数字其一就返回。根据两个返回值判断结果。
```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == p || root == q || root == null) return root;
        TreeNode left = lowestCommonAncestor(root.left, p , q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        
        if (left != null && right != null) return root;
        if (left == null) return right;
        else return left;
    }
}
```
