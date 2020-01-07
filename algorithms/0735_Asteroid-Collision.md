#  Asteroid Collisionh
------------------
@ [Description](https://leetcode.com/problems/asteroid-collision/)  
@ Tags: Stack     
@ Medium

------------------
## Solution
时间复杂度：$O(N)$  
空间复杂度：$O(N)$
```java
class Solution {
    public int[] asteroidCollision(int[] asteroids) {
        Stack<Integer> stack = new Stack<>();
        for (int item : asteroids) {
            if (stack.isEmpty() || stack.peek() * item > 0 || stack.peek() < 0 && item > 0 )
                stack.push(item);
            else {
                boolean flag = true;
                while (!stack.isEmpty() && stack.peek() * item < 0) {
                    if (Math.abs(stack.peek()) > Math.abs(item)) {
                        flag = false;
                        break;
                    } else if (Math.abs(stack.peek()) == Math.abs(item)) {
                        stack.pop();
                        flag = false;
                        break;
                    } else {
                        stack.pop();
                    }
                }
                if (flag)
                    stack.push(item);
            }
        }
        int[] res = new int[stack.size()];
        while (!stack.isEmpty())
            res[stack.size() - 1] = stack.pop();
        return res;
    }
}
```
