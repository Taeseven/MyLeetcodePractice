# Flatten Nested List Iterator
------------------
@ [Description](https://leetcode.com/problems/flatten-nested-list-iterator/)  
@ Tags: Stack, Design    
@ Medium

------------------
## Solution
Queue + Preprocess  
```java
public class NestedIterator implements Iterator<Integer> {
    private Queue<Integer> queue;
    
    public NestedIterator(List<NestedInteger> nestedList) {
        queue = new LinkedList<>();
        pushToStack(nestedList);
    }
    
    private void pushToStack(List<NestedInteger> nestedList) {
        for (NestedInteger item : nestedList) {
            if (item.isInteger())
                queue.offer(item.getInteger());
            else 
                pushToStack(item.getList());
        }
    }

    @Override
    public Integer next() {
        return queue.poll();
    }

    @Override
    public boolean hasNext() {
        return !queue.isEmpty();
    }
}
```
