# Divide Two Integers
------------------
@ [Description](https://leetcode.com/problems/divide-two-integers/)  
@ Tags: Bit Operation  
@ Medium

------------------
## Solution
本题的关键是不等使用乘除法运算，因而我们可以采取位运算。当左移一位时就相当于乘以2。要注意当我们使用对Integer.MIN_VALUE使用$Math.abs()$时，由于溢出的问题其值为Integer.MIN_VALUE， 因而我们要将两个数casting到long.
```java
class Solution {
    public int divide(int dividend, int divisor) {
        if (dividend == Integer.MIN_VALUE && divisor == -1)
            return Integer.MAX_VALUE;
        int d = Math.abs(dividend);
        int f = Math.abs(divisor);
        int result = 0;
        while (d >= f) {
            int tmp = f, multi = 1;
            while (d >= tmp << 1) {
                tmp <<= 1;
                multi <<= 1;
            }
            d -= tmp;
            result += multi;
        }
        return (dividend < 0) ^ (divisor < 0) ? -result : result; 
    }
}
```
如果都将其转为负数可以避免使用$Math.abs()$，从而避免使用long。

