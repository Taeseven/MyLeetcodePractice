# Pow(x, n)
@ [Description](https://leetcode.com/problems/powx-n/)  
@ Tags: Math, Binary Search  
@ Medium

------------------
## Solution - Binary Search
利用二分法快速得到结果
```java
class Solution {
    public double myPow(double x, int n) {
        if (n < 0) {
            x = 1 / x;
            n = -n;
        }
        return powHelper(x, n);
        
    }
    private double powHelper(double x, int n) {
        if (n == 0) return 1.0;
        double half = powHelper(x, n/2);
        if (n % 2 == 0) return half * half;
        else return half * half * x;
    }
}
```
