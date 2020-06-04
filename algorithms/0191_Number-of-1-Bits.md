# Number of 1 Bits
------------------
@ [Description](https://leetcode.com/problems/number-of-1-bits/)  
@ Tags: Bit Manipulation   
@ Easy

------------------
## Solution
当n & (n-1)时，会将n最右端为1的值置为0，其他的各位保持不变。因此只要不断的进行&操作直至其为0即可求得为1的位数之和。这种方法不需要遍历每一位。  
时间和空间复杂度均为$O(1)$
```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        int sum = 0;
        while (n != 0) {
            sum++;
            n &= (n - 1);
        }
        return sum;
    }
}
```
