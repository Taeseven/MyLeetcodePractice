# Backspace String Compare
------------------
@ [Description](https://leetcode.com/problems/backspace-string-compare/)  
@ Tags: Stack, Two pointers     
@ Easy

------------------
## Solution 1 - Build 2 String
直接根据条件建立两个string，看其是否相等即可。  
时间复杂度：$O(M+N)$  
空间复杂度：$O(M+N)$  

## Solution 2 - Two Pointers
用两个指针从后面traverse，记录需要跳过的个数，判断新的指针是否满足条件即可。  
时间复杂度：$O(M+N)$  
空间复杂度：$O(1)$ 
```java
class Solution {
    public boolean backspaceCompare(String S, String T) {
        int s = S.length() - 1, t = T.length() - 1;
        int skip_s = 0, skip_t = 0;
        while (s >=0 || t >= 0) {
            while (s >= 0) {
                if (S.charAt(s) == '#') {skip_s++; s--;}
                else if (skip_s > 0) {skip_s--; s--;}
                else break;
            }
            while (t >= 0) {
                if (T.charAt(t) == '#') {skip_t++; t--;}
                else if (skip_t > 0) {skip_t--; t--;}
                else break;
            }
            
            if (s >= 0 && t >= 0 && S.charAt(s) != T.charAt(t))
                return false;
            if ( (s >= 0) != (t >= 0))
                return false;
            s--;
            t--;
        }
        return true;
    }
}
```
