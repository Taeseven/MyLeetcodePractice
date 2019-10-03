# Delete Node in a BST
------------------
@ [Description](https://leetcode.com/problems/delete-node-in-a-bst/)  
@ Tags: Tree   
@ Medium

------------------
## Solution
首先寻找要删除的节点。  
然后寻找该节点左子树最大值或右子树最小值与之替换。
```java
class Solution {
    public TreeNode deleteNode(TreeNode root, int key) {
        if (root == null) return root;
        if (root.val < key) root.right = deleteNode(root.right, key);
        else if (root.val > key) root.left = deleteNode(root.left, key);
        else {
            if (root.left == null && root.right == null) return null;
            else if (root.left != null) {
                root.val = largestSmall(root);
                root.left = deleteNode(root.left, root.val);
            } else {
                root.val = smallestLarge(root);
                root.right = deleteNode(root.right, root.val);
            }
        }
        return root;
    }
    
    private Integer largestSmall(TreeNode root) {
        root = root.left;
        while (root.right != null) root = root.right;
        return root.val;
    }
    
    private Integer smallestLarge(TreeNode root) {
        root = root.right;
        while (root.left != null) root = root.left;
        return root.val;
    }
}
```
整理后的简便解法：
```java
    public TreeNode deleteNode(TreeNode root, int key) {
        if(root==null) return null;
        if(root.val > key) {root.left=deleteNode(root.left,key);}
        else if(root.val < key) {root.right=deleteNode(root.right,key);}
        else {
            if(root.left==null || root.right==null){//左节点或右节点为空，或为叶子节点
                root=(root.left==null) ? root.right : root.left;
            }else{//左、右节点都不为空的情况下，寻找右子树的最左节点赋值给当前结点，再将右子树的最左节点删除
                TreeNode curNode=root.right;
                while(curNode.left!=null) curNode=curNode.left;
                root.val=curNode.val;
                root.right=deleteNode(root.right,curNode.val);
            }
        }
        
        return root;
    }
```
