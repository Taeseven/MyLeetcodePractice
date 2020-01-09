# Minimum Window Substring
------------------
@ [Description](https://leetcode.com/problems/minimum-window-substring/)  
@ Tags: Hash Table, Two Pointers, String, Sliding Window   
@ Hard

------------------
## Solution
利用hash table记录所需的字符以及当前窗口的字符统计，滑动两个指针已得到结果。  
时间空间复杂度均为$O(|S|+|T|)$  
```java
class Solution {
    public String minWindow(String s, String t) {
        if (s.length() == 0 || t.length() == 0)
            return "";
        Map<Character, Integer> dictT = new HashMap<>();
        for (char c : t.toCharArray())
            dictT.put(c, dictT.getOrDefault(c, 0) + 1);
        
        int l = 0, r = 0;
        int formed = 0, required = dictT.size();
        int start = 0, end = Integer.MAX_VALUE;
        Map<Character, Integer> window = new HashMap<>();
        while (r < s.length()) {
            char c = s.charAt(r);
            window.put(c, window.getOrDefault(c, 0) + 1);
            if (dictT.containsKey(c) && window.get(c).intValue() == dictT.get(c).intValue())
                formed++;
            
            while (l <= r && formed == required) {
                c = s.charAt(l);
                if (r - l < end - start) {
                    end = r;
                    start = l;
                }
                window.put(c, window.get(c) - 1);
                if (dictT.containsKey(c) && window.get(c).intValue() < dictT.get(c).intValue())
                    formed--;
                l++;
            }
            r++;
        }
        return (end == Integer.MAX_VALUE) ? "" : s.substring(start, end + 1);
    }
}
```
The **Integer.intValue()** is used to get the primitive int value of Integer. The other test cases pass for you because the int values are low and the auto-unboxing feature of java does the value comparison for you. But for this one test case the int values are pretty large and hence it leads to object comparison instead of the value comparison which is not what we want.
