# Letter Combinations of a Phone Number
------------------
@ [Description](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)  
@ Tags: String, Backtracking  
@ Medium

------------------
## Solution
```java
class Solution {
    String[] map = {"abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
    List<String> letters = new ArrayList<>();
    
    public List<String> letterCombinations(String digits) {
        if (digits.length() == 0) return letters;
        combineHelper(digits, "");
        return letters;
    }
    private void combineHelper(String digits, String tmp) {
        if (tmp.length() == digits.length()) {
            letters.add(tmp);
            return;
        }
        for (int i = 0; i < map[digits.charAt(tmp.length()) - '2'].length(); i++)
            combineHelper(digits, tmp + map[digits.charAt(tmp.length()) - '2'].charAt(i));
    }
}
```
