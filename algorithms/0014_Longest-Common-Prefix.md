# Reverse Integer
---------------
@[Description](https://leetcode.com/problems/longest-common-prefix/)  
@ Easy
---------------
## Solution

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        int len = strs.length;
        if (len == 0) return "";
        int minLen = Integer.MAX_VALUE;
        for (String s : strs) minLen = Math.min(minLen, s.length());
        for (int i = 0; i < minLen; i++) {
            for (int j = 1; j < len; j++) {
                if (strs[0].charAt(i) != strs[j].charAt(i)) return strs[0].substring(0, i);
            }
        }
        return strs[0].substring(0, minLen);
    }
}
```