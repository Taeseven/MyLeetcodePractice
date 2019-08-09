# Valid Parentheses
------------------
@ [Description](https://leetcode.com/problems/valid-parentheses/)  
@ Tags: Stack  
@ Easy 

------------------
## Solution - Stack
Stack有Last-In-First-Out的性质，可以运用在本题目中。如果字符长度为奇数必然不满足条件，同时注意要考虑空栈的问题。
```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();
        if (s.length() % 2 != 0) return false;
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (c == '(' || c == '[' || c == '{') stack.push(c);
            else if (stack.isEmpty()) return false;
            else {
                char pop = stack.pop();
                if (c == ')' && pop != '(') return false;
                else if (c == '}' && pop != '{') return false;
                else if (c == ']' && pop != '[') return false;
            }        
        }
        return stack.isEmpty();
    }
}
```