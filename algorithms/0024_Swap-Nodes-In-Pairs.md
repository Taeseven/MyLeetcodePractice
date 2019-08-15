# Swap Nodes in Pairs
------------------
@ [Description](https://leetcode.com/problems/swap-nodes-in-pairs/)  
@ Tags: Linked List  
@ Medium

------------------
## Solution 1 - Recursion
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode swapPairs(ListNode head) {
        if (head == null || head.next == null) return head;
        ListNode tmp = head.next;
        head.next = swapPairs(tmp.next);
        tmp.next = head;
        return tmp;
    }
}
```

## Solution 2 - Loop
```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        ListNode preHead = new ListNode(0), curr = preHead;
        preHead.next = head;
        while (curr.next != null && curr.next.next != null) {
            ListNode tmp = curr.next.next;
            curr.next.next = tmp.next;
            tmp.next = curr.next;
            curr.next = tmp;
            curr = curr.next.next;
        }
        return preHead.next;
    }
}
```
