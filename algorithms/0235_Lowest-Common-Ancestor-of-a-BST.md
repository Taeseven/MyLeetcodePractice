# Lowest Common Ancestor of a Binary Search Tree
@ [Description](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)  
@ Tags: Tree        
@ Easy

------------------
## Solution
```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        while (root != null) {
            if (root.val > p.val && root.val > q.val) {
                root = root.left;
            } else if (root.val < p.val && root.val < q.val) {
                root = root.right;
            } else {
                return root;
            }
        }
        return null;
    }
}
```
