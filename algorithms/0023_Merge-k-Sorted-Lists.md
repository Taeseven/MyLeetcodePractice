# Merge k Sorted Lists
------------------
@ [Description](https://leetcode.com/problems/merge-k-sorted-lists/)  
@ Tags: Linked List, Divide and Conquer, Heap   
@ Hard

------------------
## Solution 1 - Heap
只需要当前k个list的第一个node放在MinHeap中即可。  
时间复杂度：$O(NlogK)$  
空间复杂度：$O(K)$  
```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        ListNode head = new ListNode(0);
        ListNode curr = head;
        PriorityQueue<ListNode> pq = new PriorityQueue(new Comparator<ListNode>() {
            public int compare(ListNode n1, ListNode n2) {
                return n1.val - n2.val;
            }
        });
        for (ListNode node : lists) {
            if (node != null)
                pq.offer(node);
        }
        while (!pq.isEmpty()) {
            ListNode tmp = pq.poll();
            curr.next = new ListNode(tmp.val);
            curr = curr.next;
            if (tmp.next != null)
                pq.offer(tmp.next);
        }
        return head.next;
    }
}
```

## Solution 2 - Divid and Conquer
时间复杂度：$O(NlogK)$  
空间复杂度：$O(K)$ 
```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists.length == 0)
            return null;
        return mergeHelper(lists, 0, lists.length - 1);
    }
    
    private ListNode mergeHelper(ListNode[] list, int start, int end) {
        if (start == end)
            return list[start];
        int mid = start + (end - start) / 2;
        ListNode left = mergeHelper(list, start, mid);
        ListNode right = mergeHelper(list, mid + 1, end);
        return merge(left, right);
    }
    
    private ListNode merge(ListNode n1, ListNode n2) {
        ListNode head = new ListNode(0);
        ListNode curr = head;
        while (n1 != null && n2 != null) {
            if (n1.val < n2.val) {
                curr.next = n1;
                curr = curr.next;
                n1 = n1.next;
            } else {
                curr.next = n2;
                curr = curr.next;
                n2 = n2.next;
            }
        }
        if (n1 != null) {
            curr.next = n1;
        } else {
            curr.next = n2;
        }
        return head.next;
    }
}
```
