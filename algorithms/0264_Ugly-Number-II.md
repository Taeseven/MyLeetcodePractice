#  Ugly Number
------------------
@ [Description](https://leetcode.com/problems/ugly-number-ii/)  
@ Tags: Math, DP, Heap    
@ Medium

------------------
## Solution 1 - Heap
```java
class Solution {
    public int nthUglyNumber(int n) {
        PriorityQueue<Long> pq = new PriorityQueue<>();
        HashSet<Long> see = new HashSet<>();
        pq.offer(1L);
        see.add(1L);
        int[] prime = new int[]{2, 3, 5};
        while (true) {
            Long curr = pq.poll();
            n--;
            if (n == 0)
                return curr.intValue();
            for (int i : prime) {
                long new_ = curr * i;
                if (!see.contains(new_)) {
                    see.add(new_);
                    pq.offer(new_);
                }
            }
        }
    }
}
```

## Solution 2 - DP
```java
class Solution {
    public int nthUglyNumber(int n) {
        int[] dp = new int[n];
        dp[0] = 1;
        int i2 = 0, i3 = 0, i5 = 0;
        for (int i = 1; i < n; i++) {
            int next = Math.min(Math.min(2*dp[i2], 3*dp[i3]), 5*dp[i5]);
            dp[i] = next;
            if (next == 2*dp[i2]) i2++;
            if (next == 3*dp[i3]) i3++;
            if (next == 5*dp[i5]) i5++;
        }
        return dp[n - 1];
    }
}
```
