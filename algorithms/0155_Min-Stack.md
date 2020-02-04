# Min Stack
------------------
@ [Description](https://leetcode.com/problems/min-stack/)  
@ Tags: Stack, Design    
@ Easy

------------------
## Solution
考虑每个节点不仅要存当前数值，同时还要存之前所有数中的最小值。两个数为一组构成stack中的元素，因此还要考虑有个全局的最小值。
```java
class MinStack {
    private Stack<Integer> stack;
    private int min;
    
    /** initialize your data structure here. */
    public MinStack() {
        stack = new Stack<>();
        min = Integer.MAX_VALUE;
    }
    
    public void push(int x) {
        stack.push(min);
        min = Math.min(x, min);
        stack.push(x);
    }
    
    public void pop() {
        stack.pop();
        min = stack.pop();
    }
    
    public int top() {
        return stack.peek();
    }
    
    public int getMin() {
        return min;
    }
}
```
