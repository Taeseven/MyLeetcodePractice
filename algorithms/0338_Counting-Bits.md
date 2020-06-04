# Counting Bits
------------------
@ [Description](https://leetcode.com/problems/counting-bits/)  
@ Tags: Bit Manipulation, DP   
@ Medium

------------------
## Solution - Rightmost "1" Bit
思想和191类似，找到n&(n - 1)的值加一即可。  
时间和空间复杂度均为$O(n)$  
```java
class Solution {
    public int[] countBits(int num) {
        int[] res = new int[num + 1];
        for (int i = 1; i <= num; i++) {
            res[i] = res[i & (i - 1)] + 1;
        }
        return res;
    }
}
