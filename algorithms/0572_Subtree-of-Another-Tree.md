# Subtree of Another Tree
---------------
@[Description](https://leetcode.com/problems/subtree-of-another-tree/)  
@ Tag: Tree  
@ Easy

---------------
## Solution 1 - Recursion
时间复杂度：$O(MN)$  
```java
class Solution {
    public boolean isSubtree(TreeNode s, TreeNode t) {
        if (s == null)
            return t == null;
        return isSame(s, t) || isSubtree(s.left, t) || isSubtree(s.right, t);
    }
    private boolean isSame(TreeNode s, TreeNode t) {
        if (s == null && t == null) return true;
        if (s == null || t == null) return false;
        if (s.val != t.val) return false;
        return isSame(s.left, t.left) && isSame(s.right, t.right);
    }
}
```

## Solution 2 - DFS
```java
class Solution {
    List<TreeNode> list = new ArrayList<>();
    
    public boolean isSubtree(TreeNode s, TreeNode t) {
        dfs(s, t);
        if (list.isEmpty()) return false;
        for (int i = 0; i < list.size(); i++) {
            if (compare(list.get(i), t))
                return true;
        }
        return false;
        
    }
    
    private boolean compare(TreeNode s, TreeNode t) {
        if (s == null && t == null) return true;
        if (s == null || t == null) return false;
        if (s.val != t.val) return false;
        return compare(s.left, t.left) && compare(s.right, t.right);
    }
    
    private void dfs(TreeNode s, TreeNode t) {
        if (s == null) return;
        if (s.val == t.val)
            list.add(s);
        dfs(s.left, t);
        dfs(s.right, t);
    }
}
```
