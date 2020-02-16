# Longest Substring with At Least K Repeating Characters
------------------
@ [Description](https://leetcode.com/problems/longest-substring-with-at-least-k-repeating-characters/)  
@ Tags:    
@ Medium

------------------
## Solution
利用recursion思想。如果某一char的count小于要求那么其一定不在所要的结果中，那么只需要以该char为节点再对左右两边进行search即可。  
时间复杂度：$O(N^2)$ ?
```java
class Solution {
    public int longestSubstring(String s, int k) {
        if (s == null || s.length() == 0)
            return 0;
        int[] count = new int[26];
        for (int i = 0; i < s.length(); i++)
            count[s.charAt(i) - 'a']++;
        boolean flag = true;
        for (int i = 0; i < 26; i++) {
            if (count[i] != 0 && count[i] < k)
                flag = false;
        }
        if (flag)
            return s.length();
        int begin = 0, end = 0, res = 0;
        while (end < s.length()) {
            if (count[s.charAt(end) - 'a'] < k) {
                res = Math.max(res, longestSubstring(s.substring(begin, end), k));
                begin = end + 1;
            }
            end++;
        }
        res = Math.max(res, longestSubstring(s.substring(begin), k));
        return res;
    }
}
```
