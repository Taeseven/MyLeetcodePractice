# Flatten 2D Vector
------------------
@ [Description](https://leetcode.com/problems/flatten-2d-vector/)  
@ Tags: Design    
@ Medium

------------------
## Solution 1 - Queue
Queue + Preprocess  
```java
class Vector2D {
    private Queue<Integer> queue;
    public Vector2D(int[][] v) {
        queue = new LinkedList<>();
        for (int[] list : v) {
            for (int i : list)
                queue.offer(i);
        }
    }
    
    public int next() {
        return queue.poll();
    }
    
    public boolean hasNext() {
        return !queue.isEmpty();
    }
}
```
