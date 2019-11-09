# LRU Cache
------------------
@ [Description](https://leetcode.com/problems/lru-cache/)  
@ Tags: Design    
@ Hard

------------------
## Solution
首先需要一个HashMap实现查询的操作。  
每次插入需要将其放在最前，每次查询后也需要将其挪到最前。若超过了容量还需要将最末的元素删除。  
考虑不断的讲元素移位的操作，我们可以考虑使用双向链表处理。HashMap键所对应的时双向链表中的node。
```java
class LRUCache {
    class DLinkNode {
        int key;
        int val;
        DLinkNode prev;
        DLinkNode next;
    }
    private Map<Integer, DLinkNode> cache = new HashMap<>();
    private int capacity, size;
    private DLinkNode head, tail;

    public LRUCache(int capacity) {
        this.capacity = capacity;
        size = 0;
        head = new DLinkNode();
        tail = new DLinkNode();
        head.next = tail;
        head.prev = tail;
        tail.prev = head;
        tail.next = head;
    }
    
    public int get(int key) {
        DLinkNode node = cache.get(key);
        if (node == null)
            return -1;
        moveToHead(node);
        return node.val;
    }
    
    public void put(int key, int value) {
        DLinkNode node = cache.get(key);
        if (node == null) {
            DLinkNode newNode = new DLinkNode();
            newNode.key = key;
            newNode.val = value;
            cache.put(key, newNode);
            add(newNode);
            size++;
            if (size > capacity) {
                DLinkNode pop = popLast();
                cache.remove(pop.key);
                size--;
            }
        } else {
            node.val = value;
            moveToHead(node);
        }
    }
    
    private void moveToHead(DLinkNode node) {
        remove(node);
        add(node);
    }
    private void add(DLinkNode node) {
        node.next = head.next;
        node.prev = head;
        head.next.prev = node;
        head.next = node;
    }
    private void remove(DLinkNode node) {
        DLinkNode prev = node.prev;
        DLinkNode next = node.next;
        prev.next = next;
        next.prev = prev;
    }
    private DLinkNode popLast() {
        DLinkNode res = tail.prev;
        DLinkNode prev = res.prev;
        prev.next = tail;
        tail.prev = prev;
        return res;
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
 ```
