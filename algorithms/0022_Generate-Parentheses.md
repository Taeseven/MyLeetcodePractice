# Generate Parentheses
------------------
@ [Description](https://leetcode.com/problems/generate-parentheses/)  
@ Tags: String, Backtracking  
@ Medium

------------------
## Solution 1 - Backtracking
Time Complexity: $O(\frac{4^n}{\sqrt{n}})$  
Space Complexity: $O(\frac{4^n}{\sqrt{n}})$  
```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> list = new ArrayList<>();
        if (n == 0) return null;
        helper(list, n, 0, "");
        return list;
    }
    private void helper(List<String> list, int leftRemain, int rightNeed, String curr) {
        if (leftRemain == 0 && rightNeed == 0) {
            list.add(curr);
            return;
        }
        if (leftRemain > 0) helper(list, leftRemain-1, rightNeed+1, curr+'(');
        if (rightNeed > 0) helper(list, leftRemain, rightNeed-1, curr+')');
        
    }
}
```

## Solution 2 - Dynamic Programming
利用动态规划的思想，我们发现有：  
$f(0) = ""$  
$f(1) = (f(0))$  
$f(2) = (f(0))f(1) + (f(1))f(0)$  
$f(3) = (f(0))f(2) + (f(1))f(1) + (f(2))f(0)$  
$\cdots$  
$f(n) = (f(0))f(n-1) + (f(1))f(n-2) + \cdots + (f(n-1))f(0)$  
由此我们可以利用list储存$f(0),\cdots,f(n-1)$进而求得$f(n)$  
时间及空间复杂度？？？？
```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<List<String>> lists = new ArrayList<>();
        lists.add(Collections.singletonList(""));
        for (int i = 1; i <= n; i++) {
            List<String> list = new ArrayList<>();
            for (int j = 0; j < i; j++) {
                for (String a : lists.get(j)) {
                    for (String b : lists.get(i - j - 1))
                        list.add('(' + a + ')' + b);
                }
            }
            lists.add(list);
        }
        return lists.get(n);
    }
}
```
