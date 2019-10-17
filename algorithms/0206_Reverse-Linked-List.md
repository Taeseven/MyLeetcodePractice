#  Reverse Linked List
------------------
@ [Description](https://leetcode.com/problems/reverse-linked-list/)  
@ Tags: Linked List   
@ Easy

------------------
## Solution
```java
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode node = new ListNode(0);
        node.next = head;
        ListNode prev = null;
        while (head != null) {
            ListNode tmp = head.next;
            head.next = prev;
            prev = head;
            head = tmp;
        }
        node.next = prev;
        return node.next;
    }
}
```
