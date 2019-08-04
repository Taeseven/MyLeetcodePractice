# Add Two Numbers
------------------
@ [Description](https://leetcode.com/problems/add-two-numbers/)  

------------------
* 注意进位问题  
* 当位数不同时，其中一个ListNode会先移动到末尾，此时注意不能用.next，要进行判断  
* ```int x = (p != null) ? p.val : 0; ``` 若p不为null则x值为p.val，反之则将其值赋为0
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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        int add_on = 0;
        ListNode p = l1, q = l2;
        ListNode result = new ListNode(0);
        ListNode curr = result;
        while (p != null || q != null || add_on != 0) {
            int x = (p != null) ? p.val : 0;
            int y = (q != null) ? q.val : 0;
            int sum = x + y + add_on;
            add_on = sum / 10;
            curr.next = new ListNode(sum % 10);
            curr = curr.next;
            if (p != null) p = p.next;
            if (q != null) q = q.next;
        }
        return result.next;
    }
}
```