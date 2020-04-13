# Jump Game
------------------
@ [Description](https://leetcode.com/problems/jump-game/)  
@ Tags: Array, Greedy    
@ Medium

------------------
## Solution
记录当前位置可以到达的最远距离即可。  
时间复杂度：$O(N)$  
空间复杂度：$O(1)$  
```java
class Solution {
    public boolean canJump(int[] nums) {
        int dest = nums.length - 1, maxIdx = nums[0];
        for (int i = 1; i < nums.length - 1; i++) {
            if (maxIdx < i) return false;
            if (maxIdx >= dest) return true;
            maxIdx = Math.max(maxIdx, i + nums[i]);
        }
        return maxIdx >= dest;
    }
}
```
