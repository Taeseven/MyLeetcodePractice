#  Concatenated Words
------------------
@ [Description](https://leetcode.com/problems/concatenated-words/)  
@ Tags: DP, DFS, Trie     
@ Hard

------------------
## Solution - DFS
时间复杂度：$O(N^2)$  
空间复杂度：$O(N)$  
```java
class Solution {
    public List<String> findAllConcatenatedWordsInADict(String[] words) {
        Set<String> set = new HashSet<>();
        List<String> res = new ArrayList<>();
        int min = Integer.MAX_VALUE;
        for (String s : words) {
            if (s.length() == 0)
                continue;
            set.add(s);
            min = Math.min(min, s.length());
        }
        for (String s : words) {
            if (dfs(set, s, 0, min))
                res.add(s);
        }
        return res;
    }
    private boolean dfs(Set<String> set, String s, int start, int min) {
        for (int i = start + min; i <= s.length() - min; i++) {
            if (set.contains(s.substring(start, i)) && (set.contains(s.substring(i)) || dfs(set, s, i, min)))
                return true;
        }
        return false;
    }
    
}
```
