#  Implement Queue using Stacks
------------------
@ [Description](https://leetcode.com/problems/implement-queue-using-stacks/)  
@ Tags: Stack, Design    
@ Easy

------------------
## Solution
利用两个stack，从一个stack pop并push到另一个stack后顺序即正确。  
如果pop只从第二个stack出，即可降低时间复杂度。  
```java
class MyQueue {
    private Stack<Integer> s1;
    private Stack<Integer> s2;
    private int front;

    /** Initialize your data structure here. */
    public MyQueue() {
        s1 = new Stack<>();
        s2 = new Stack<>();
    }
    
    /** Push element x to the back of queue. */
    public void push(int x) {
        if (s1.isEmpty())
            front = x;
        s1.push(x);
    }
    
    /** Removes the element from in front of queue and returns that element. */
    public int pop() {
        if (s2.isEmpty()) {
            while (!s1.isEmpty())
                s2.push(s1.pop());
        }
        return s2.pop();
    }
    
    /** Get the front element. */
    public int peek() {
        if (!s2.isEmpty())
            return s2.peek();
        return front;
    }
    
    /** Returns whether the queue is empty. */
    public boolean empty() {
        return s1.isEmpty() && s2.isEmpty();
    }
}
```
