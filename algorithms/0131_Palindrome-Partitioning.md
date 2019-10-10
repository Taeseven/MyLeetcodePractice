# Palindrome Partitioning
------------------
@ [Description](https://leetcode.com/problems/palindrome-partitioning/)  
@ Tags: Backtracking   
@ Medium

------------------
## Solution - DFS
```java
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> res = new ArrayList<>();
        if (s == null || s.length() == 0)
            return res;
        helper(s, 0, new ArrayList<String>(), res);
        return res;
    }
    private void helper(String s, int start, ArrayList<String> tmp, List<List<String>> res) {
        if (s.length() == start) {
            res.add(new ArrayList<String>(tmp));
            return;
        }
        
        for (int i = start; i <  s.length(); i++) {
            String subString = s.substring(start, i+1);
            if (isPalindrome(subString)) {
                tmp.add(subString);
                helper(s, i+1, tmp, res);
                tmp.remove(tmp.size() - 1);
            }
        }
    }
    
    private boolean isPalindrome(String s) {
        int i = 0;
        int j = s.length() - 1;
        while (i < j) {
            if (s.charAt(i) != s.charAt(j))
                return false;
            i++;
            j--;
        }
        return true;
    }
}
```
该段代码可以利用dp的思想提升check是否为回文串的效率，目前存在冗余。
