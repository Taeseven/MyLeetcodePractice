# Edit Distance
------------------
@ [Description](https://leetcode.com/problems/edit-distance/)  
@ Tags: DP, String   
@ Hard

------------------
## Solution
dp[i][j] indicate the distance between first i char of word1 and first j char of word2. Thus, if word1[i] == word2[j], dp[i][j] = min(1 + dp[i-1][j], 1 + dp[i][j-1], dp[i][j]). And if word1[i] != word2[j] we can still calculate dp[i][j] based on dp[i-1][j]. dp[i][j-1] and dp[i][j].  
时间及空间复杂度均为$O(mn)$  
```java
class Solution {
    public int minDistance(String word1, String word2) {
        int n = word1.length(), m = word2.length();
        // if one of the word is empty
        if (n * m == 0) {
            return n + m;
        }
        
        int[][] dp = new int[n + 1][m + 1];
        // first column and row
        for (int i = 0; i < n + 1; i++) {
            dp[i][0] = i;
        }
        for (int i = 0; i < m + 1; i++) {
            dp[0][i] = i;
        }
        
        for (int i = 1; i < n + 1; i++) {
            for (int j = 1; j < m + 1; j++) {
                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    dp[i][j] = Math.min(dp[i - 1][j - 1],
                                       1 + Math.min(dp[i][j - 1], dp[i - 1][j]));
                } else {
                    dp[i][j] = 1 + Math.min(dp[i - 1][j - 1],
                                       Math.min(dp[i][j - 1], dp[i - 1][j]));
                }
            }
        }
        return dp[n][m];
    }
}
```
