# Construct Binary Search Tree from Preorder Traversal
------------------
@ [Description](https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/)  
@ Tags: Tree     
@ Medium

------------------
## Solution
根据大小关系分配到新的左右子树即可。
```java
class Solution {
    public TreeNode bstFromPreorder(int[] preorder) {
        if (preorder == null || preorder.length == 0)
            return null;
        return helper(preorder, 0, preorder.length - 1);
    }
    private TreeNode helper(int[] preorder, int start, int end) {
        if (start > end)
            return null;
        TreeNode root = new TreeNode(preorder[start]);
        if (start == end)
            return root;
        for (int i = start + 1; i <= end; i++) {
            if (preorder[i] > root.val) {
                root.left = helper(preorder, start + 1, i - 1);
                root.right = helper(preorder, i, end);
                return root;
            }
        }
        root.left = helper(preorder, start + 1, end);
        return root;
    }
}
```
