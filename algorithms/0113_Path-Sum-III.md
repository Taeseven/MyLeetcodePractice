# Path Sum II
@ [Description](https://leetcode.com/problems/path-sum-ii/)  
@ Tags: Tree, DFS               
@ Medium

------------------
## Solution
注意用ArrayList处理时，helper执行末尾需要将最后一个元素移除，才能输出正确的path，不然则会输出类似preorder的序列。  
时间及空间复杂度均为：$O(N)$  
存在问题：用stack替换List进行操作时，runtime较慢，不知道原因为何？  
```java
class Solution {
    List<List<Integer>> res = new ArrayList<>();
    
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        if (root == null) return res;
        List<Integer> curr = new ArrayList<>();
        helper(root, sum, curr);
        return res;
    }
    
    private void helper(TreeNode root, int sum, List<Integer> curr) {
        if (root == null) return;
        curr.add(root.val);
        if (root.left == null && root.right == null) {
            if (sum == root.val) {
                res.add(new ArrayList<Integer>(curr));
            }
        }
        helper(root.left, sum - root.val, curr);
        helper(root.right, sum - root.val, curr);
        curr.remove(curr.size() - 1);
    }
}
```
