# Binary Tree Longest Consecutive Sequence
@ [Description](https://leetcode.com/problems/binary-tree-longest-consecutive-sequence/)  
@ Tags: Tree        
@ Medium

------------------
## Solution
以根节点为切入点，若左子树或右子树可以与根节点构成连续的序列则长度加1，同时注意更新最大值。分治法实现。  
时间和空间复杂度都是$O(N)$.    
```java
class Solution {
    private int res = 0;
    public int longestConsecutive(TreeNode root) {
        helper(root);
        return res;
    }
    
    private int helper(TreeNode root) {
        if (root == null) return 0;
        
        int tmp = 1;
        int left = helper(root.left);
        int right = helper(root.right);
        if ( (left != 0 && root.val + 1== root.left.val) && (right != 0 && root.val + 1== root.right.val)) {
            tmp += Math.max(right, left);
        } else if (left != 0 && root.val + 1== root.left.val) {
            tmp += left;
        } else if (right != 0 && root.val + 1== root.right.val) {
            tmp += right;
        }
        
        if (tmp > res) res = tmp;
        return tmp;
    }
}
```
