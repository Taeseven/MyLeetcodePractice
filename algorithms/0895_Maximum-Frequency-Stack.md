#  Maximum Frequency Stack
------------------
@ [Description](https://leetcode.com/problems/maximum-frequency-stack/)  
@ Tags: Hash Table, Stack    
@ Hard

------------------
## Solution
时间复杂度：$O(1)$  
空间复杂度：$O(N)$  
```java
class FreqStack {
    Map<Integer, Integer> freq;
    Map<Integer, Stack<Integer>> stacks;
    int max;

    public FreqStack() {
        freq = new HashMap<>();
        stacks = new HashMap<>();
        max = 0;
    }
    
    public void push(int x) {
        int i = freq.getOrDefault(x, 0) + 1;
        freq.put(x, i);
        max = Math.max(max, i);
        stacks.putIfAbsent(i, new Stack());
        stacks.get(i).push(x);
        
    }
    
    public int pop() {
        int res = stacks.get(max).pop();
        freq.put(res, freq.get(res) - 1);
        if (stacks.get(max).isEmpty())
            max--;
        return res;
    }
}
```
