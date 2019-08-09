# Roman To Integer
--------------------
@[Description](https://leetcode.com/problems/roman-to-integer/)  
@ Easy
---------------
## Solution
注意考虑4，9，40，90，400和900的特殊情况即可。
```java
class Solution {
    public int romanToInt(String s) {
        int sum = 0;
        for (int i = 0; i < s.length() - 1; i++){
            if (charToInt(s.charAt(i)) < charToInt(s.charAt(i + 1))) sum -= charToInt(s.charAt(i));
            else sum += charToInt(s.charAt(i));
        }
        sum += charToInt(s.charAt(s.length() - 1));
        return sum;
        
    }
    private int charToInt(char c) {
        if (c == 'I') return 1;
        if (c == 'V') return 5;
        if (c == 'X') return 10;
        if (c == 'L') return 50;
        if (c == 'C') return 100;
        if (c == 'D') return 500;
        if (c == 'M') return 1000;
        return -1;
    }
}
```
如果将前一字符存起来只需遍历一遍即可，上段代码需要遍历两遍。
```java
class Solution {
    public int romanToInt(String s) {
        if (s == null || s.length() == 0) return 0;
        char prev = ' ';
        int number = 0;
        for(int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            number = getNumber(number, prev, c);
            prev = c;
        }
        
        return number;        
    }
    
    private int getNumber(int number, char prev, char current) {
        if (prev == 'I' && current == 'V') return number - 1 + 4;
        if (prev == 'I' && current == 'X') return number - 1 + 9;
        if (prev == 'X' && current == 'L') return number - 10 + 40;
        if (prev == 'X' && current == 'C') return number - 10 + 90;
        if (prev == 'C' && current == 'D') return number - 100 + 400;
        if (prev == 'C' && current == 'M') return number - 100 + 900;
        if (current == 'I') return number + 1;
        if (current == 'V') return number + 5;
        if (current == 'X') return number + 10;
        if (current == 'L') return number + 50;
        if (current == 'C') return number + 100;
        if (current == 'D') return number + 500;
        if (current == 'M') return number + 1000;
        return number;
    }
}
```
