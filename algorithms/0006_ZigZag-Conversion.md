# Valid Parentheses
------------------
@ [Description](https://leetcode.com/problems/zigzag-conversion/)  
@ Tags: String  
@ Medium

------------------
## Solution
找规律即可。  
首尾两行每个周期重复一次，其余各行每周期重复两次，且步长变化。用StringBuilder可以节省内存的使用。
```java
class Solution {
    public String convert(String s, int numRows) {
        if (numRows <= 1) return s;
        int T = 2 * (numRows - 1);
        StringBuilder zigzag = new StringBuilder();
        for (int i = 0; i < s.length(); i += T) zigzag.append(s.charAt(i));
        for (int i = 1; i < numRows - 1; i++) {
            int step = 2 * i;
            for (int j = i; j < s.length(); j += step) {
                zigzag.append(s.charAt(j));
                step = T - step;
            }
        }
        for (int i = numRows - 1; i < s.length(); i += T) zigzag.append(s.charAt(i));
        return zigzag.toString();
    }
}
```