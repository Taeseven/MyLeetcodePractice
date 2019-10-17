#  Reverse Linked List II
------------------
@ [Description](https://leetcode.com/problems/reverse-linked-list/)  
@ Tags: Linked List   
@ Medium

------------------
## Solution
```java
class Solution {
    public ListNode reverseBetween(ListNode head, int m, int n) {
        ListNode node = new ListNode(0);
        node.next = head;
        head = node;
        ListNode prev_ = head;
        for (int i = 0; i < m; i++) {
            prev_ = head;
            head = head.next;
        }
        ListNode prev = null;
        for (int i = m; i <= n; i++) {
            ListNode tmp = head.next;
            head.next = prev;
            prev = head;
            head = tmp;
        }
        prev_.next.next = head;
        prev_.next = prev;
        return node.next;
    }
}
```
