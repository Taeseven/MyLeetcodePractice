# Valid Anagram
@ [Description](https://leetcode.com/problems/valid-anagram/)  
@ Tags: Hash Table           
@ Easy

------------------
## Solution
分别记录每个字符串出现的字符及个数，进行比对。  
时间复杂度：$O(N)$  
空间复杂度：$O(1)$  
```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false;
        int[] count = new int[26];
        for (int i = 0; i < s.length(); i++) {
            count[s.charAt(i) - 'a']++;
        }
        for (int i = 0; i < t.length(); i++) {
            count[t.charAt(i) - 'a']--;
            if (count[t.charAt(i) - 'a'] < 0) return false; 
        }
        return true;
    }
}
```
