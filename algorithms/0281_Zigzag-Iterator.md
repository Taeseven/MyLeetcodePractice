# Zigzag Iterator
------------------
@ [Description](https://leetcode.com/problems/zigzag-iterator/)  
@ Tags: Design    
@ Medium

------------------
## Solution
利用queue和iterator
```java
public class ZigzagIterator {
    Queue<Iterator> queue;
    public ZigzagIterator(List<Integer> v1, List<Integer> v2) {
        queue = new LinkedList<>();
        if (!v1.isEmpty()) 
            queue.offer(v1.iterator());
        if (!v2.isEmpty()) 
            queue.offer(v2.iterator());
    }

    public int next() {
        Iterator tmp = queue.poll();
        int result = (Integer) tmp.next();
        if (tmp.hasNext())
            queue.offer(tmp);
        return result;
    }

    public boolean hasNext() {
        return !queue.isEmpty();
    }
}
```
