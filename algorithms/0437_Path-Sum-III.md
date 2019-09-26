# Path Sum III
@ [Description](https://leetcode.com/problems/path-sum-iii/)  
@ Tags: Tree             
@ Medium

------------------
## Solution
并不是最快的解法，最快可能需要用到map。
```java
class Solution {
    int total = 0;
    public int pathSum(TreeNode root, int sum) {
        if (root == null) return total;
        helper(root, sum);
        pathSum(root.right, sum);
        pathSum(root.left, sum);
        return total;
        
    }
    
    private void helper(TreeNode root, int sum) {
        if (root == null) return;
        if (root.val == sum) total++;
        helper(root.left, sum - root.val);
        helper(root.right, sum - root.val);
    }
}
```
