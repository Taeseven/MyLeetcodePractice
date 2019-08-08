# Palindrome Number
-------------------
@[Description](https://leetcode.com/problems/palindrome-number/)  
@ Easy  

------------------
## Solution
对于负数肯定以及末位为0的非零正数，其肯定不是非负数，可以直接输出false；对于其余情况可以求取其逆序以判断二者是否相等。  
然而对于一个回文数，我们其实只需要求其长度一半的逆序进行比较即可，注意存在位数为奇数的情况。

```java
class Solution {
    public boolean isPalindrome(int x) {
        if (x < 0 || (x != 0 && x % 10 == 0)) return false;
        int res = 0;
        int half = 0;
        for (; x > half; x /= 10) half = half * 10 + x % 10;
        return half == x || half / 10 == x;
    }
}
```