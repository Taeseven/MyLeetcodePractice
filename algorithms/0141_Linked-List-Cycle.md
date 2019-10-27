#  Linked List Cycle
------------------
@ [Description](https://leetcode.com/problems/linked-list-cycle/)  
@ Tags: Linked List, Two Pointer    
@ Medium

------------------
## Solution 1 - Set
用set储存访问过的节点。  
时间空间复杂度均为$O(N)$  
```java
public class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null)
            return false;
        Set<ListNode> seen = new HashSet<>();
        while (head != null) {
            if (seen.contains(head))
                return true;
            else
                seen.add(head);
            head = head.next;
        }
        return false;
    }
}
```
## Solution 2 - Two Pointer
用两个快慢指针，若可相遇即存在环，空间复杂度为$O(1)$  
```java
public class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null || head.next == null) {
            return false;
        }
        ListNode slow = head;
        ListNode fast = head.next;
        while (slow != fast) {
            if (fast == null || fast.next == null) {
                return false;
            }
            slow = slow.next;
            fast = fast.next.next;
        }
        return true;
    }
}
```
