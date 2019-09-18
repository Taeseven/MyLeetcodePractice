# Binary Tree Paths
@ [Description](https://leetcode.com/problems/binary-tree-paths/)  
@ Tags: Tree, Depth first Search        
@ Easy

------------------
## Solution 1 - Traverse
```java
class Solution {
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> res = new ArrayList<>();
        if (root == null) return res;
        helper(root, Integer.toString(root.val), res);
        return res;
        
    }
    
    private void helper(TreeNode root, String path, List<String> res) {
        if (root.left == null && root.right == null) {
            res.add(path);
            return;
        }
        if (root.left != null) {
            helper(root.left, path + "->" + Integer.toString(root.left.val), res);
        }
        if (root.right != null) {
            helper(root.right, path + "->" + Integer.toString(root.right.val), res);
        }
    }
}
```

## Solution 2 - Divide & Conquer
```java
class Solution {
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> res = new ArrayList<>();
        if (root == null) return res;
        if (root.left == null && root.right == null) {
            res.add(Integer.toString(root.val));
            return res;
        }
        
        List<String> leftPaths = binaryTreePaths(root.left);
        List<String> rightPaths = binaryTreePaths(root.right);
        
        for (String s : leftPaths) 
            res.add(Integer.toString(root.val) + "->" + s);
        for (String s : rightPaths)
            res.add(Integer.toString(root.val) + "->" + s);
        
        return res;
    }
}
```
