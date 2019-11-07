# Convert Sorted List to Binary Search Tree
------------------
@ [Description](https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree/)  
@ Tags: Linked List, DFS    
@ Medium

------------------
## Solution - Find Medium One
List中间的数字是root，前面的部分是左子树，后面的部分是右子树。  
因而我们只需要将recursion遍历左右即可，注意右子树的部分需要将其与mid断开。  
时间复杂度：$O(NlogN)$  
空间复杂度：$O(logN)$
```java
class Solution {

  private ListNode findMiddleElement(ListNode head) {

    // The pointer used to disconnect the left half from the mid node.
    ListNode prevPtr = null;
    ListNode slowPtr = head;
    ListNode fastPtr = head;

    // Iterate until fastPr doesn't reach the end of the linked list.
    while (fastPtr != null && fastPtr.next != null) {
      prevPtr = slowPtr;
      slowPtr = slowPtr.next;
      fastPtr = fastPtr.next.next;
    }

    // Handling the case when slowPtr was equal to head.
    if (prevPtr != null) {
      prevPtr.next = null;
    }

    return slowPtr;
  }

  public TreeNode sortedListToBST(ListNode head) {

    // If the head doesn't exist, then the linked list is empty
    if (head == null) {
      return null;
    }

    // Find the middle element for the list.
    ListNode mid = this.findMiddleElement(head);

    // The mid becomes the root of the BST.
    TreeNode node = new TreeNode(mid.val);

    // Base case when there is just one element in the linked list
    if (head == mid) {
      return node;
    }

    // Recursively form balanced BSTs using the left and right halves of the original list.
    node.left = this.sortedListToBST(head);
    node.right = this.sortedListToBST(mid.next);
    return node;
  }
}
```

## Solution 2 - Inorder
利用inorder的思想，只需要遍历一遍得到总长度即可，不断的平分List。  
记录head的值，当start>end时将head赋值给root，head向后走一步即可。  
时间复杂度：$O(N)$  
空间复杂度：$O(logN)$
```java
class Solution {
    ListNode head;
    public TreeNode sortedListToBST(ListNode head) {
        if (head == null)
            return null;
        ListNode p = head;
        int len = 0;
        while (p != null) {
            p = p.next;
            len++;
        }
        this.head = head;
        return helper(0, len - 1);
    }
    private TreeNode helper(int start, int end) {
        if (start > end)
            return null;
        int mid = start + (end - start) / 2;
        TreeNode left = helper(start, mid - 1);
        TreeNode root = new TreeNode(this.head.val);
        this.head = this.head.next;
        TreeNode right = helper(mid + 1, end);
        root.left = left;
        root.right = right;
        return root;
    }
}
```
