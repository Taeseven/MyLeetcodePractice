#  Longest Palindromic Substring
------------------
@ [Description](https://leetcode.com/problems/longest-palindromic-substring/)  
@ Tags: DP, String   
@ Medium

------------------
## Solution 1 - DP
用一个二维的dp矩阵判断i j间是否为回文，同时用两个指针储存当前最长长度回文子串的起始位置。  
时间复杂度：$O(N^2)$  
空间复杂度：$O(N^2)$
```java
class Solution {
    public String longestPalindrome(String s) {
        if (s.length() == 0)
            return "";
        boolean[][] dp = new boolean[s.length()][s.length()];
        int start = 0, end = 0;
        
        for (int i = 0; i < s.length(); i++) {
            for (int j = i; j >= 0; j--) {
                if (i == j)
                    dp[i][j] = true;
                else if (i - j == 1)
                    dp[i][j] = (s.charAt(i) == s.charAt(j));
                else if (s.charAt(i) == s.charAt(j) && dp[i-1][j+1])
                    dp[i][j] = true;
                
                if (dp[i][j] && i - j > end - start) {
                    end = i;
                    start = j;
                }
            }
        }
        return s.substring(start, end + 1);
    }
}
```

## Solution 2 
从某一位置利用两个指针分别向两个方向延伸。空间复杂度降低到$O(1)$.
```java
class Solution {
    public String longestPalindrome(String s) {
        if (s == null || s.length() == 0)
            return "";
        int start = 0, end = 0;
        for (int i = 0; i < s.length(); i++) {
            int len1 = helper(s, i, i);
            int len2 = helper(s, i, i + 1);
            int len = Math.max(len1, len2);
            if (len > end - start) {
                start = i - (len - 1) / 2;
                end = i + len / 2;
            }
        }
        return s.substring(start, end + 1);
    }
    private int helper(String s, int left, int right) {
        while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
            left--;
            right++;
        }
        return right - left - 1;
    }
}
```
