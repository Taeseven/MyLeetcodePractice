# Longest Substring with At Most Two Distinct Characters
------------------
@ [Description](https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/)  
@ Tags: Hash Table, Two Pointers, String, Sliding Window    
@ Medium

------------------
## Solution - Two Pointer + Hash Map
时间复杂度：$O(N)$  
```java
class Solution {
    public int lengthOfLongestSubstringTwoDistinct(String s) {
        if (s.length() < 3)
            return s.length();
        int res = 0;
        int i = 0, j = 0;
        HashMap<Character, Integer> map = new HashMap<>();
        for (; i < s.length(); i++) {
            while (j < s.length() && (map.size() < 2 || map.containsKey(s.charAt(j)))) {
                map.put(s.charAt(j), map.getOrDefault(s.charAt(j), 0) + 1);
                j++;
            }
            res = Math.max(res, j - i);
            if (map.get(s.charAt(i)) == 1)
                map.remove(s.charAt(i));
            else
                map.put(s.charAt(i), map.get(s.charAt(i)) - 1);
        }
        return res;
    }
}
```
