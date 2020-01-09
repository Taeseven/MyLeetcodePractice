# Gas Station
------------------
@ [Description](https://leetcode.com/problems/gas-station/)  
@ Tags: Greedy     
@ Medium

------------------
## Solution
可行起点必须是gas大于cost的点，同时总体的gas要大于cost，遍历一遍即可。时间复杂度$O(N)$  
```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int total = 0, curr = 0, start = 0;
        for (int i = 0; i < gas.length; i++) {
            total += gas[i] - cost[i];
            curr += gas[i] - cost[i];
            if (curr < 0) {
                start = i + 1;
                curr = 0;
            }
        }
        return (total >= 0) ? start : -1;
    }
}
```
