#  Linked List Cycle II
------------------
@ [Description](https://leetcode.com/problems/linked-list-cycle-ii/)  
@ Tags: Linked List, Two Pointer    
@ Medium

------------------
## Solution
先用两个快慢指针判断是否存在环；  
若存在环，将head与fast两个指针按步长为1的速率同时移动，直到相遇，相遇的点即为环的起点。  
```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        if (head == null || head.next == null) {
            return null;
        }
        ListNode fast = head;
        ListNode slow = head;
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
            if (fast == slow) {
                while (head != fast) {
                    head = head.next;
                    fast = fast.next;
                }
                return head;
            }
        }
        return null;
    }
}
```
