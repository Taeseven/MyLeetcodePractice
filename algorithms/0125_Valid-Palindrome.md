#  Valid Palindrome
------------------
@ [Description](https://leetcode.com/problems/valid-palindrome/)  
@ Tags: String, Two Pointers     
@ Easy

------------------
## Solution
```java
class Solution {
    public boolean isPalindrome(String s) {
        if (s == null || s.length() == 0)
            return true;
        int l = 0, r = s.length() - 1;
        char head, tail;
        while (l <= r) {
            head = s.charAt(l);
            tail = s.charAt(r);
            if (!Character.isLetterOrDigit(head))
                l++;
            else if (!Character.isLetterOrDigit(tail))
                r--;
            else {
                if (Character.toLowerCase(head) != Character.toLowerCase(tail))
                    return false;
                l++;
                r--;
            }
        }
        return true;
    }
}
```
