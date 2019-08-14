# Remove Nth Node From End of List
------------------
@ [Description](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)  
@ Tags: Linked List, Two Pointer  
@ Medium

------------------
## Solution
利用两个指针，第一个指针先走n步，随后两个指针一起想链表末端移动的，当第一个指针到达链表末端时，第二个指针的下一项刚好为要删除的项。  
需注意删除的项恰好为第一项时需特别处理。
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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode firstPointer = head, secondPointer = head;
        for (int i = 0; i < n; i++) firstPointer = firstPointer.next;
        if (firstPointer == null) return head.next;
        while (firstPointer.next != null) {
            firstPointer = firstPointer.next;
            secondPointer = secondPointer.next;
        }
        secondPointer.next = secondPointer.next.next;
        return head;
    }
}
```
