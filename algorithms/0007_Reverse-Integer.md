# Reverse Integer
---------------
@[Description](https://leetcode.com/problems/reverse-integer/)  
@ Easy
---------------
## Solution
注意逆序存在溢出的情况，因而将结果保存在long中最后返回时做判断。
```java
class Solution {
    public int reverse(int x) {
        long res = 0;
        for (; x !=  0; x /= 10) res = res * 10 + x % 10;
        return (res > Integer.MAX_VALUE || res < Integer.MIN_VALUE) ? 0 : (int)res;
    }
}
```