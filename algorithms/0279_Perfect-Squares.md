# Perfect Squares
------------------
@ [Description](https://leetcode.com/problems/perfect-squares/)  
@ Tags: Math, DP, BFS   
@ Medium

------------------
## Solution 1 - DP
时间复杂度$O(n\sqrt{n})$  
空间复杂度$O(n)$   
```java
class Solution {
    public int numSquares(int n) {
        int[] dp = new int[n + 1];
        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[0] = 0;
        dp[1] = 1;
        
        for (int i = 2; i <= n; i++) {
            for (int j = 1; j * j <= i; j++) {
                dp[i] = Math.min(dp[i], dp[i - j * j] + 1);
            }
        }
        return dp[n];
    }
}
```

## Solution 2 - BFS
不断减去所有小于n的完全平方数，直至余数中存在完全平方数。  
时间和空间复杂度$O(n^{\frac{h}{2}})$, [具体分析](https://leetcode.com/problems/perfect-squares/solution/)。  
```java
class Solution {
    public int numSquares(int n) {
        Set<Integer> set = new HashSet<>();
        set.add(n);
        
        ArrayList<Integer> square = new ArrayList<>();
        for (int i = 1; i * i <= n; i++) {
            square.add(i * i);
        }
        
        int cnt = 0;
        while (set.size() > 0) {
            cnt += 1;
            Set<Integer> next_set = new HashSet<>();
            for (Integer remainder : set) {
                for (Integer square_num : square) {
                    if (remainder.equals(square_num)) {
                        return cnt;
                    } else if (remainder > square_num) {
                        next_set.add(remainder - square_num);
                    }
                }
            }
            set = next_set;
        }
        return cnt;
    }
}
```

## Solution 3 - Math
[详解](https://leetcode.com/problems/perfect-squares/solution/)   
时间复杂度$O(\sqrt{n})$  
空间复杂度$O(1)$
```java
class Solution {

  protected boolean isSquare(int n) {
    int sq = (int) Math.sqrt(n);
    return n == sq * sq;
  }

  public int numSquares(int n) {
    // four-square and three-square theorems.
    while (n % 4 == 0)
      n /= 4;
    if (n % 8 == 7)
      return 4;

    if (this.isSquare(n))
      return 1;
    // enumeration to check if the number can be decomposed into sum of two squares.
    for (int i = 1; i * i <= n; ++i) {
      if (this.isSquare(n - i * i))
        return 2;
    }
    // bottom case of three-square theorem.
    return 3;
  }
}
```
