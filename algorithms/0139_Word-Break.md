# Word Break
------------------
@ [Description](https://leetcode.com/problems/word-break/)  
@ Tags: DP    
@ Nedium

------------------
## Solution
时间复杂度：$O(N^2)$  
空间复杂度：$O(N)$  
```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        Set<String> dict = new HashSet(wordDict);
        boolean[] dp = new boolean[s.length() + 1];
        dp[0] = true;
        for (int i = 1; i <= s.length(); i++) {
            for (int j = 0; j < i; j++) {
                if (dp[j] && dict.contains(s.substring(j, i))) {
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[s.length()];
    }
}
```
