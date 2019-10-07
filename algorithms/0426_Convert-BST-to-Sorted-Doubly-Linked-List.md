# Convert Binary Search Tree to Sorted Doubly Linked List
------------------
@ [Description](https://leetcode.com/problems/convert-binary-search-tree-to-sorted-doubly-linked-list/)  
@ Tags: Linked List, Divide and Conquer, Tree   
@ Medium

------------------
## Solution
输出其实为Inorder的顺序，首先要找到最小的节点，然后利用first和last两个node不断的travers回去，并再最后将首尾相连即可。  
时间复杂度及空间复杂度均为：$O(N)$  
```java
class Solution {
    Node first = null;
    Node last = null;
    public Node treeToDoublyList(Node root) {
        if (root == null) return null;
        
        helper(root);
        first.left = last;
        last.right = first;
        return first;
    }
    
    private void helper(Node root) {
        if (root != null) {
            helper(root.left);
            if (last == null)
                first = root;
            else {
                last.right = root;
                root.left = last;
            }
            last = root;
            
            helper(root.right);
        }
    }
    
}
```
