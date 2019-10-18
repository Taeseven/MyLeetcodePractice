#  Partition List
------------------
@ [Description](https://leetcode.com/problems/partition-list/)  
@ Tags: Linked List, Two Pointer    
@ Medium

------------------
## Solution
将List分为两部分重新构造。注意末尾node的next要重置为null，不然会嵌套。  
时间复杂度：$O(N)$  
空间复杂度：$O(1)$
```java
class Solution {
    public ListNode partition(ListNode head, int x) {
        if (head == null || head.next == null)
            return head;
        ListNode before = new ListNode(0);
        ListNode after = new ListNode(0);
        ListNode before_ = before;
        ListNode after_ = after;
        while (head != null) {
            if (head.val < x) {
                before.next = head;
                before = before.next;
            } else {
                after.next = head;
                after = after.next;
            }
            head = head.next;
        }
        after.next = null;
        before.next = after_.next;
        return before_.next;
    }
}
```
