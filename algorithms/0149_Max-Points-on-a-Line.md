# Max Points on a Line
------------------
@ [Description](https://leetcode.com/problems/max-points-on-a-line/)  
@ Tags: Hash Table, Math     
@ Hard

------------------
## Solution
遍历计算每对点的斜率，若有公共点切斜率一致时则共线。  
需要注意的时直接储存斜率可能存在精度的问题，因而可以考虑求其计算斜率的dx，dy的最大公约数，记录dx/d和dy/d即可。同时由于用int[]记录时返回的会是reference即地址因此在判断map中是否包含该斜率时会出错，这里我考虑采用String的形势来记录。  
时间复杂度：$O(N^2)$  
空间复杂度：$O(N)$
```java
class Solution {
    public int maxPoints(int[][] points) {
        int N = points.length;
        int max = 0;
        for (int i = 0; i < N; i++) {
            int same = 1;
            int tmp = 0;
            Map<String, Integer> count = new HashMap<>();
            for (int j = i + 1; j < N; j++) {
                if (points[i][0] == points[j][0] && points[i][1] == points[j][1])
                    same++;
                else {
                    String k = slope(points[i], points[j]);
                    int c = count.getOrDefault(k, 0);
                    count.put(k, c + 1);
                    tmp = Math.max(tmp, c + 1);
                }
            }
            max = Math.max(max, tmp + same);
        }
        return max;
    }
    
    private String slope (int[] p1, int[] p2) {
        String res = "";
        int dx = p1[0] - p2[0];
        int dy = p1[1] - p2[1];
        if (dx == 0) res = String.valueOf(p1[0]) + String.valueOf(0);
        else if (dy == 0) res = String.valueOf(0) + String.valueOf(p1[1]);
        else {
            int d = gcd(dx, dy);
            res = String.valueOf(dx/d) + String.valueOf(dy/d);
        }
        return res;
    }
    
    private int gcd(int dx, int dy) {
        return dy == 0 ? dx : gcd(dy, dx % dy);
    }
}
```
