# Binary Tree Postorder Traversal
@ [Description](https://leetcode.com/problems/binary-tree-postorder-traversal/)  
@ Tags: Tree, Stack        
@ Hard

------------------
## Solution 1 - Stack
用一个stack储存遍历tree。  
时间复杂度：$O(N)$  
空间复杂度：$O(N)$  
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if (root == null) return res;
        Stack<TreeNode> stack = new Stack<>();
        TreeNode curr = root;
        TreeNode pre = null;
        stack.push(root);
        
        while (!stack.empty()) {
            curr = stack.peek();
            if (pre == null || pre.left == curr || pre.right == curr) {
                if (curr.left != null) stack.push(curr.left);
                else if (curr.right != null) stack.push(curr.right);
            } else if (curr.left == pre) {
                if (curr.right != null) stack.push(curr.right);
            } else {
                res.add(curr.val);
                stack.pop();
            }
            pre = curr;
        }
        return res;
    }
}
```
使用Linked List可以简便一些。要注意，需要使用addFirst()所以必须声明为LinkedList。  
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        LinkedList<Integer> res = new LinkedList<>();
        if (root == null) return res;
        stack.add(root);
        
        while (!stack.empty()) {
            TreeNode node = stack.pop();
            res.addFirst(node.val);
            if (node.left != null) stack.push(node.left);
            if (node.right != null) stack.push(node.right);
        }
        return res;
    }
}
```


## Solution 2 - Recurrison
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        helper(root, res);
        return res;
    }
    
    private void helper(TreeNode root, List<Integer> res) {
        if (root == null) return;
        helper(root.left, res);
        helper(root.right, res);
        res.add(root.val);
    } 
}
```
