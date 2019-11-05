# Construct Binary Tree from Inorder and Postorder Traversal
------------------
@ [Description](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)  
@ Tags: Array, Tree, DFS     
@ Medium

------------------
## Solution
```java
class Solution {
    Map<Integer, Integer> map;
    int[] pre;
    int[] in;
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        map = new HashMap<>();
        pre = preorder;
        in = inorder;
        for (int i = 0; i < in.length; i++)
            map.put(in[i], i);
        return helper(0, 0, 0, inorder.length);
    }
    private TreeNode helper(int p, int i, int j, int n) {
        if (n <= 0)
            return null;
        TreeNode root = new TreeNode(pre[p]);
        if (n == 1)
            return root;
        int k = map.get(pre[p]);
        int l = k - i;
        root.left = helper(p+1, i, k-1, l);
        root.right = helper(p+l+1, k+1, j, n-l-1);
        return root;
    }
}
```
