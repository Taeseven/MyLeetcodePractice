#  Reorder List
------------------
@ [Description](https://leetcode.com/problems/reorder-list/)  
@ Tags: Linked List    
@ Medium

------------------
## Solution
题目相当于将List后半部分倒序插在前半部分中，因为可以将过程分为几部：  
  1. 找到List的middle位置
  2. 将middle位置后面的后半部分reverse
  3. 用两个指针分别从head和middle移动，不断将后半部分插入到前半部分，知道前指针与middle相遇

```java
class Solution {
    public void reorderList(ListNode head) {
        if (head == null || head.next == null)
            return;
        // find the middle
        ListNode p1 = head;
        ListNode p2 = head;
        while (p2.next != null && p2.next.next != null) {
            p1 = p1.next;
            p2 = p2.next.next;
        }
        
        // reverse the second half
        // 1 -> 2 -> 3 -> 5 -> 4
        ListNode middle = p1;
        p1 = p1.next;
        ListNode prev = null;
        while (p1 != null) {
            ListNode tmp = p1.next;
            p1.next = prev;
            prev = p1;
            p1 = tmp;
        }
        middle.next = prev;
        
        // reorder
        p1 = head;
        p2 = middle;
        while (p1 != middle) {
            ListNode tmp = p2.next;
            p2.next = (p2.next != null) ? p2.next.next : null;
            ListNode tmp2 = p1.next;
            p1.next = tmp;
            tmp.next = tmp2;
            p1 = tmp2;
        }
        return;
    }
}
```
