# Balanced Binary Tree
@ [Description](https://leetcode.com/problems/balanced-binary-tree/)  
@ Tags: Tree, Depth first Search        
@ Easy

------------------
## Solution
直接判断每个节点左右子树是否balanced即可。  
```java
class Solution {
    boolean res = true;
    public boolean isBalanced(TreeNode root) {
        helper(root);
        return res;
    }
    
    private int helper(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int l = helper(root.left);
        int r = helper(root.right);
        if (Math.abs(l - r) > 1) res = false;
        return Math.max(l, r) + 1;
    }
}
```
