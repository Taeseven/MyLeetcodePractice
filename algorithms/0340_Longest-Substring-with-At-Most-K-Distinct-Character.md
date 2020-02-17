# Longest Substring with At Most K Distinct Characters
------------------
@ [Description](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/)  
@ Tags: Hash Table, String, Sliding Window    
@ Hard

------------------
## Solution
Two pointer遍历，利用hashmap存当前window下字符和count。  
时间复杂度：$O(N)$  
空间复杂度：$O(k)$  
```java
class Solution {
    public int lengthOfLongestSubstringKDistinct(String s, int k) {
        if (k < 1)
            return k;
        int i = 0, j = 0;
        int res = 0;
        HashMap<Character, Integer> map = new HashMap<>();
        for (; i < s.length(); i++) {
            while (j < s.length() && (map.size() < k || map.containsKey(s.charAt(j)))) {
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
