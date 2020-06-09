# Reverse String
------------------
@ [Description](https://leetcode.com/problems/reverse-string/)  
@ Tags: Two Pointers, String   
@ Easy

------------------
## Solution
```java
class Solution {
    public void reverseString(char[] s) {
        int left = 0, right = s.length - 1;
        while (left < right) {
            char tmp = s[left];
            s[left] = s[right];
            s[right] = tmp;
            left++;
            right--;
        }
    }
}
```
