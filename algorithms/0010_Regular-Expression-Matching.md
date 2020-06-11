# Regular Expression Matching
------------------
@ [Description](https://leetcode.com/problems/regular-expression-matching/)  
@ Tags: String, Backtracking, DP  
@ Hard

------------------
## Solution
时间空间复杂度均为$O(n)$  
```java
class Solution {
    public boolean isMatch(String s, String p) {
        // edge case
        if (s == null || p == null) {
            return false;
        }
        
        boolean[][] dp = new boolean[p.length() + 1][s.length() + 1];
        // (0, 0) is True
        dp[0][0] = true;
        for (int i = 1; i <= p.length(); i++) {
            if (i > 1 && p.charAt(i - 1) == '*') {
                dp[i][0] = dp[i - 2][0];
            }
        }
        
        for (int i = 1; i <= p.length(); i++) {
            for (int j = 1; j <= s.length(); j++) {
                if (p.charAt(i - 1) == s.charAt(j - 1) || p.charAt(i - 1) == '.') {
                    dp[i][j] = dp[i - 1][j - 1];
                } else if (p.charAt(i - 1) == '*') {
                    // repeat
                    if (p.charAt(i - 2) == s.charAt(j - 1) || p.charAt(i - 2) == '.') {
                        dp[i][j] = dp[i][j - 1] || dp[i - 2][j];
                    } else {
                        dp[i][j] = dp[i - 2][j];
                    }
                }
            }
        }
        return dp[p.length()][s.length()];
    }
}
```
