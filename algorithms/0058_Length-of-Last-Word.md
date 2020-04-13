# Length of Last Word
------------------
@ [Description](https://leetcode.com/problems/length-of-last-word/)  
@ Tags: String    
@ Easy

------------------
## Solution
```java
class Solution {
    public int lengthOfLastWord(String s) {
        int len = 0, idx = s.length();
        while (idx > 0) {
            idx--;
            if (s.charAt(idx) != ' ') len++;
            else if (len > 0) return len;
        }
        return len;
    }
}
```
