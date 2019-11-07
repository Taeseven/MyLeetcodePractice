# Binary Tree Maximum Path Sum
------------------
@ [Description](https://leetcode.com/problems/binary-tree-maximum-path-sum/)  
@ Tags: Tree, DFS    
@ Hard

------------------
## Solution
注意path可以不包含root和叶节点。  
我们考虑有个全局的max去记录当前最大的，它会记录以当前点为转折点的最大path sum。返回时需要注意的时我们只应该返回当前node和他的一条最大的子path。
时间复杂度：$O(N)$  
空间复杂度：$O(logN)$  
```java
class Solution {
    int max = Integer.MIN_VALUE;
    public int maxPathSum(TreeNode root) {
        helper(root);
        return max;
    }
    private int helper(TreeNode root) {
        if (root == null)
            return 0;
        int left = Math.max(helper(root.left), 0);
        int right = Math.max(helper(root.right), 0);
        max = Math.max(left+right+root.val, max);
        return root.val + Math.max(left, right);
    }
}
```
