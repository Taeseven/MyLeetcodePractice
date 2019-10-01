# Binary Search Tree Iterator
------------------
@ [Description](https://leetcode.com/problems/binary-search-tree-iterator/)  
@ Tags: Tree  
@ Medium

------------------
## Solution
时间复杂度：$O(H)$   
空间复杂度：$O(1)$  
```java
class Solution {
    public TreeNode insertIntoBST(TreeNode root, int val) {
        TreeNode pre = root;
        TreeNode tmp = root;
        while (tmp != null) {
            if (tmp.val < val) {
                pre = tmp;
                tmp = tmp.right;
            } else {
                pre = tmp;
                tmp = tmp.left;
            }
        }
        if (pre.val < val) pre.right = new TreeNode(val);
        else pre.left = new TreeNode(val);
        return root;
    }
}
```
