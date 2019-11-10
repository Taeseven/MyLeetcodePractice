# LFU Cache
------------------
@ [Description](https://leetcode.com/problems/lfu-cache/)  
@ Tags: Design    
@ Hard

------------------
## Solution
与LRU Cache类似，但是此时还需要记录每个node被访问的频率。  
可以考虑增加一个map，key：出现次数，value：双向链表记录该频率下的所有node。若有访问则将其在当前链表中去除，加在频率+1所对应链表的head。
```java
class LFUCache {
    class Node {
        int key, val;
        int freq;
        Node prev, next;
        public Node(int key, int val) {
            this.key = key;
            this.val = val;
            freq = 1;
        }
    }
    class DList {
        Node head, tail;
        int size;
        public DList() {
            head = new Node(0,0);
            tail = new Node(0,0);
            head.next = tail;
            tail.prev = head;
            size = 0;
        }
        public void addHead(Node node) {
            node.prev = head;
            node.next = head.next;
            head.next.prev = node;
            head.next = node;
            size++;
        }
        public void remove(Node node) {
            Node prev = node.prev;
            Node next = node.next;
            prev.next = next;
            next.prev = prev;
            size--;
        }
        public void removeLast() {
            Node tmp = tail.prev;
            cache.remove(tmp.key);
            remove(tmp);
        }
    }
    
    private int capacity, size;
    private Map<Integer, Node> cache;
    private Map<Integer, DList> freq;
    private int max_freq;
    
    public LFUCache(int capacity) {
        this.capacity = capacity;
        size = 0;
        max_freq = 0;
        cache = new HashMap<>();
        freq = new HashMap<>();
    }
    
    public int get(int key) {
        Node node = cache.get(key);
        if (node == null) 
            return -1;
        int tmp_freq = node.freq;
        DList prevList = freq.get(tmp_freq);
        prevList.remove(node);
        node.freq++;
        max_freq = Math.max(tmp_freq+1, max_freq);
        DList currList = freq.getOrDefault(tmp_freq + 1, new DList());
        currList.addHead(node);
        freq.put(tmp_freq, prevList);
        freq.put(tmp_freq+1, currList);
        return node.val;
    }
    
    public void put(int key, int value) {
        if (capacity == 0)
            return;
        if (cache.get(key) != null) {
            cache.get(key).val = value;
            get(key);
            return;
        }
        Node node = new Node(key, value);
        DList currList = freq.getOrDefault(1, new DList());
        currList.addHead(node);
        cache.put(key, node);
        size++;
        if (size > capacity) {
            if (currList.size > 1) {
                currList.removeLast();
            } else {
                for (int i = 2; i <= max_freq; i++) {
                    if (freq.get(i) != null && freq.get(i).size > 0) {
                        freq.get(i).removeLast();
                        break;
                    }
                }
            }
            size--;
        }
        freq.put(1, currList);
    }
}

/**
 * Your LFUCache object will be instantiated and called as such:
 * LFUCache obj = new LFUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
 ```
