#  Happy Number
------------------
@ [Description](https://leetcode.com/problems/happy-number/)  
@ Tags: Hash Table, Math    
@ Easy

------------------
## Solution
注意可能会存在loop，将所见到的数值存起来即可。  
时间空间复杂度为：$O(logN)$  
```java
class Solution {
    public boolean isHappy(int n) {
        Set<Integer> seen = new HashSet<>();
        while (n != 1 && !seen.contains(n)) {
            seen.add(n);
            n = next(n);
        }
        return n == 1;
    }
    private int next(int n) {
        int res = 0;
        while (n > 0) {
            int t = n % 10;
            n = n / 10;
            res += t * t;
        }
        return res;
    }
}
```
也可以利用快慢指针的方法降低空间复杂度。
