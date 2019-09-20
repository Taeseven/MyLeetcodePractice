# First Unique Character in a String
@ [Description](https://leetcode.com/problems/first-unique-character-in-a-string/)  
@ Tags: String, Hash Table          
@ Easy

------------------
## Solution
```java
class Solution {
    public int firstUniqChar(String s) {
        int[] times = new int[26];
        char[] chars = s.toCharArray();
        for (char ch : chars) {
            times[ch - 'a']++;
        }
        for (int i = 0; i < chars.length; i++) {
            if (times[chars[i] - 'a'] == 1)
                return i;
        }
        return -1;
    }
}
```
