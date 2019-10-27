#  Sort List
------------------
@ [Description](https://leetcode.com/problems/sort-list/)  
@ Tags: Linked List, Sort     
@ Medium

------------------
## Solution - Merge Sort
```java
class Solution {
    public ListNode sortList(ListNode head) {
        if (head == null || head.next == null)
            return head;
        ListNode slow = head;
        ListNode fast = head;
        ListNode prev = slow;
        while (fast != null && fast.next != null) {
            prev = slow;
            slow = slow.next;
            fast = fast.next.next;
        }
        prev.next = null;
        ListNode node1 = sortList(head);
        ListNode node2 = sortList(slow);
        return merge(node1, node2);
    }
    
    private ListNode merge(ListNode l1, ListNode l2) {
        ListNode head = new ListNode(0);
        ListNode curr = head;
        while (l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                curr.next = l1;
                l1 = l1.next;
            } else {
                curr.next = l2;
                l2 = l2.next;
            }
            curr = curr.next;
        }
        curr.next = (l1 != null) ? l1 : l2;
        return head.next;
    }
}
```
