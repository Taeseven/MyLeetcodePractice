#  Copy List with Random Pointer
------------------
@ [Description](https://leetcode.com/problems/copy-list-with-random-pointer/)  
@ Tags: Hash Table, Linked List    
@ Medium

------------------
## Solution
正常用HashMap的话会有$O(N)$的空间复杂度，考虑如何只使用$O(1)$的空间。  
考虑先将原list中每个nodec opy一个新的node，即：  
1 -> 2 -> 3 -> null 变为 1 -> 1' -> 2 -> 2' -> 3 -> 3' -> null  
然后再重新将每个copy出的node的random指针指向copy后的node  
最后将整个list split成两部分即可。  
时间复杂度$O(N)$
```java
// java version
class Solution {
    public Node copyRandomList(Node head) {
        if (head == null)
            return null;
        copyNext(head);
        copyRandom(head);
        return split(head);
    }
    
    private void copyNext(Node head) {
        while (head != null) {
            Node tmp = new Node(head.val);
            tmp.next = head.next;
            tmp.random = head.random;
            head.next = tmp;
            head = head.next.next;
        }
    }
    
    private void copyRandom(Node head) {
        while (head != null) {
            if (head.random != null) {
                head.next.random = head.random.next;
            }
            head = head.next.next;
        }
    }
    
    private Node split(Node head) {
        Node newHead = head.next;
        while (head != null) {
            Node tmp = head.next;
            head.next = tmp.next;
            head = head.next;
            if (tmp.next != null)
                tmp.next = tmp.next.next;
        }
        return newHead;
    }
}
```



