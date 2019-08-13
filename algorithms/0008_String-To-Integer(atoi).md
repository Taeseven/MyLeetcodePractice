# String to Integer(atoi)
------------------
@ [Description](https://leetcode.com/problems/string-to-integer-atoi/)  
@ Tags: String  
@ Medium

------------------
## Solution
```java
class Solution {
    public int myAtoi(String str) {
        int i = 0, sign = 1, len = str.length();
        long num = 0;
        while (i < len && str.charAt(i) == ' ') i++;
        if (i < len && (str.charAt(i) == '-' || str.charAt(i) == '+')) {
            sign = (str.charAt(i) == '+') ? 1 : -1;
            i += 1;
        }
        for (; i < len; i++) {
            int tmp = str.charAt(i) - '0';
            if (tmp < 0 || tmp > 9) break;
            num = num * 10 + tmp;
            if (sign * num < Integer.MIN_VALUE || sign * num > Integer.MAX_VALUE)
                return sign == 1 ? Integer.MAX_VALUE : Integer.MIN_VALUE;
        }
        return sign * (int)num;
    }
}
```
