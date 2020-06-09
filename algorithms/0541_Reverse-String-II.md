# Reverse String II
------------------
@ [Description](https://leetcode.com/problems/reverse-string-ii/)  
@ Tags: Two Pointers, String   
@ Easy

------------------
## Solution
```java
class Solution {
    public String reverseStr(String s, int k) {
        char[] c = s.toCharArray();
        for (int start = 0; start < c.length; start += 2 * k) {
            int i = start;
            int j = Math.min(i + k - 1, c.length - 1);
            while (i < j) {
                char tmp = c[i];
                c[i++] = c[j];
                c[j--] = tmp;
            }
        }
        return new String(c);
    }
}
```
