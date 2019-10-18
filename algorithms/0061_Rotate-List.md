#  Rotate List
------------------
@ [Description](https://leetcode.com/problems/rotate-list/)  
@ Tags: Linked List, Two Pointers    
@ Medium

------------------
## Solution
由于k可能大于list的长度，因而可以先遍历得到list的长度，计算得出化简后需进行的变化次数。  
该过程相当于在一个环中行走k步，将其后面与之断开，返回其新的head。  
时间复杂度：$O(N)$  
空间复杂度：$O(1)$
```java
class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        if (head == null || head.next == null || k == 0)
            return head;
        ListNode dummy = new ListNode(0);
        int count = 1;
        ListNode node = head;
        while (node.next != null) {
            node = node.next;
            count += 1;
        }
        node.next = head;
        k = count - k % count - 1;
        node = head;
        for (int i = 0; i < k; i++)
            node = node.next;
        dummy.next = node.next;
        node.next = null;
        return dummy.next;
    }
}
```
