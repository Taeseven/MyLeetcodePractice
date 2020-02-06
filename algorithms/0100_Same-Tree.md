# Same Tree
------------------
@ [Description](https://leetcode.com/problems/same-tree/)  
@ Tags: Tree, DFS    
@ Easy

------------------
## Solution
时间复杂度：$O(N)$  
空间复杂度：$O(logN)$  
```java
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null && q == null)
            return true;
        if (p == null || q == null)
            return false;
        if (q.val != p.val)
            return false;
        return isSameTree(p.right, q.right) && isSameTree(p.left, q.left);
    }
}
```
