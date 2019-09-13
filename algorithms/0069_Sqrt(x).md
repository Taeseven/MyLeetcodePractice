# Pow(x, n)
@ [Description](https://leetcode.com/problems/sqrtx/)  
@ Tags: Math, Binary Search  
@ Medium

------------------
## Solution 1 - Binary Search
Time complexity: $O(logN)$  
Space complexity: $O(1)$  
```java
class Solution {
    public int mySqrt(int x) {
        if (x < 2) return x;
        int left = 1, right = x/2;
        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (mid == x / mid) return mid;
            else if (mid > x / mid) right = mid;
            else left = mid;
        }
        if (right <= x / right) return right;
        else return left;
    }
}
```

## Solution 2 - Newton Method
切线的x轴交点横坐标为下一次迭代值：  
$x_{n+1} = \frac{1}{2} (x_n + \frac{s}{x_n})$  
Time complexity: $O(logN)$  
Space complexity: $O(1)$  
```java
 class Solution {
    public int mySqrt(int x) {
        if (x < 2) return x;
        double x0 = x;
        double x1 = (x0 + x/x0) / 2.0;
        while (Math.abs(x0 - x1) >= 1) {
            x0 = x1;
            x1 = (x0 + x/x0) / 2.0;
        }
        return (int)x1;
    }
}
```
