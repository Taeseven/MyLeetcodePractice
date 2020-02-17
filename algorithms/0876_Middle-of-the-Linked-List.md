# Middle of the Linked List
------------------
@ [Description](https://leetcode.com/problems/middle-of-the-linked-list/)  
@ Tags: Linked List    
@ Easy

------------------
## Solution
快慢指针问题。  
时间复杂度：$O(N)$  
空间复杂度：$O(1)$  
```java
class Solution {
    public ListNode middleNode(ListNode head) {
        if (head == null)
            return null;
        ListNode slow = head, fast = head;
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        return slow;
    }
}
```
