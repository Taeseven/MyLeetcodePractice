#  Reverse Nodes in k-Group
------------------
@ [Description](https://leetcode.com/problems/reverse-nodes-in-k-group/)  
@ Tags: Linked List   
@ Hard

------------------
## Solution
```java
class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode node = new ListNode(0);
        node.next = head;
        head = node;
        while (head != null) {
            head = reverse(head, k);
        }
        return node.next;
    }
//     head -> 1 -> 2 -> ... -> k -> k+1
//     return 1 (k -> .... -> 2 -> 1 -> k+1)
    private ListNode reverse(ListNode head, int k) {
        ListNode curr = head;
        for (int i = 0; i < k; i++) {
            curr = curr.next;
            if (curr == null)
                return null;
        }
        curr = head.next;
        ListNode temp;
        ListNode prev = null;
        for (int i = 0; i < k; i++) {
            temp = curr.next;
            curr.next = prev;
            prev = curr;
            curr = temp;
        }
        ListNode res = head.next;
        head.next = prev;
        res.next = curr;
        return res;
    }
}
```