# Path Sum
@ [Description](https://leetcode.com/problems/path-sum/)  
@ Tags: Tree, DFS          
@ Easy

------------------
## Solution
分治法即可，注意判断edge case.  
```java
class Solution {
    public boolean hasPathSum(TreeNode root, int sum) {
        if (root == null) return false;
        if (root.left == null && root.right == null) {
            return sum == root.val;
        }
        return hasPathSum(root.right, sum - root.val) || hasPathSum(root.left, sum - root.val);
    }

}
```
