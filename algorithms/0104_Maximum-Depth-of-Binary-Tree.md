# Maximm Depth of Binary Tree
@ [Description](https://leetcode.com/problems/maximum-depth-of-binary-tree/)  
@ Tags: Tree, Depth first Search        
@ Easy

------------------
## Solution 1 - Traverse
```java
class Solution {
    private int max;
    
    public int maxDepth(TreeNode root) {
        max = 0;
        helper(root, 1);
        return max;
    }
    
    private void helper(TreeNode root, int depth) {
        if (root == null) return;
        if (max < depth) max = depth;
        helper(root.left, depth + 1);
        helper(root.right, depth + 1);
    }
}
```

## Solution 2 - Divide & Conquer
```java
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
    }
}
```
