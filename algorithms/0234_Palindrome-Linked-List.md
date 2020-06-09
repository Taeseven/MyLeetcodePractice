# Palindrome Linked List
------------------
@ [Description](https://leetcode.com/problems/palindrome-linked-list/)  
@ Tags: Linked List, Two Pointers   
@ Easy

------------------
## Solution
```java
class Solution {
    public boolean isPalindrome(ListNode head) {
        // edge case
        if (head == null) {
            return true;
        }
        
        // find the middle of the list
        ListNode halfNode = half(head);
        // reverse the second hald
        ListNode secondHalf = reverse(halfNode.next);
        
        ListNode firstHalf = head;
        while (secondHalf != null) {
            if (secondHalf.val != firstHalf.val) {
                return false;
            }
            secondHalf = secondHalf.next;
            firstHalf = firstHalf.next;
        }
        return true;  
    }
    
    private ListNode half(ListNode head) {
        ListNode fast = head;
        ListNode slow = head;
        while (fast.next != null && fast.next.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        return slow;
    }
    
    private ListNode reverse(ListNode head) {
        ListNode prev = null;
        ListNode curr = head;
        while (curr != null) {
            ListNode tmp = curr.next;
            curr.next = prev;
            prev = curr;
            curr = tmp;
        }
        return prev;
    }
}
```
