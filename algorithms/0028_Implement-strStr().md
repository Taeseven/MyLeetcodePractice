# Implement strStr()
------------------
@ [Description](https://leetcode.com/problems/implement-strstr/)  
@ Tags: String  
@ Easy

------------------
## Solution 1
直接遍历解决，注意由于两个for-loop的终止条件取件于字符是否相等，因而最好不要直接在for-loop的statement中限定循环的终止条件。
```java
class Solution {
    public int strStr(String haystack, String needle) {
        if (needle == null) return 0;
        int l1 = haystack.length(), l2 = needle.length();
        if (haystack == null || l1 < l2) return -1;
        for (int i = 0; ; i++) {
            if (i + l2 > l1) return -1;
            for (int j = 0; ; j++) {
                if (j == l2) return i;
                if (haystack.charAt(i + j) != needle.charAt(j)) break;
            }
        }
        
    }
}
```

## Solution 2 - subString()
调用subString()函数解决问题。
class Solution {
    public int strStr(String haystack, String needle) {
        if (needle == null) return 0;
        int l1 = haystack.length(), l2 = needle.length();
        for (int i = 0; i < l1 - l2 + 1; i++) {
            if (haystack.substring(i, i+l2).equals(needle)) return i;
        }        
        return -1;
    }
}
```