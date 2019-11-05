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
    int[] in;
    int[] post;
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        map = new HashMap<>();
        in = inorder;
        post = postorder;
        for (int i = 0; i < in.length; i++)
            map.put(in[i], i);
        return helper(0, 0, post.length - 1, post.length);
    }
    private TreeNode helper(int in_start, int post_start, int post_end, int n) {
        if (n <= 0)
            return null;
        TreeNode root = new TreeNode(post[post_end]);
        if (n == 1)
            return root;
        int k = map.get(root.val);
        int l = k - in_start;
        root.left = helper(in_start, post_start, post_start + l - 1,l);
        root.right = helper(k+1, post_start + l,post_end - 1,n - l -1);
        return root;
    }
}
```
