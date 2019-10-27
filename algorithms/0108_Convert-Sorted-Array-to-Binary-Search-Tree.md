#  Convert Sorted Array to Binary Search Tree
------------------
@ [Description](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)  
@ Tags: Tree, DFS     
@ Easy

------------------
## Solution
```java
class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {
        return helper(nums, 0, nums.length - 1);
    }
    
    private TreeNode helper(int[] nums, int left, int right) {
        if (left > right)
            return null;
        if (left == right)
            return new TreeNode(nums[left]);
        int mid = left + (right - left) / 2;
        TreeNode root = new TreeNode(nums[mid]);
        root.left = helper(nums, left, mid - 1);
        root.right = helper(nums, mid + 1, right);
        return root;
    }
}
```
