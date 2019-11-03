# Triangle
------------------
@ [Description](https://leetcode.com/problems/triangle/)  
@ Tags: Array, DP     
@ Medium

------------------
## Solution - DP
每个值只能从其上方或右上角过来，直接在输入中修改数据即可，最后遍历一遍最后一行即可。
```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        if (triangle == null || triangle.size() == 0 || triangle.get(0).size() == 0)
            return 0;
        for (int i = 0; i < triangle.size(); i++) {
            for (int j = 0; j < i + 1; j++) {
                if (i == 0 && j == 0)
                    continue;
                if (j == 0)
                    triangle.get(i).set(j, triangle.get(i).get(j) + triangle.get(i-1).get(j));
                else if (j == i)
                    triangle.get(i).set(j, triangle.get(i).get(j) + triangle.get(i-1).get(j-1));
                else
                    triangle.get(i).set(j, triangle.get(i).get(j) + Math.min(triangle.get(i-1).get(j), triangle.get(i-1).get(j-1)));
            }
        }
        int res = Integer.MAX_VALUE;
        for (int i = 0; i < triangle.size(); i++) {
            res = Math.min(res, triangle.get(triangle.size() - 1).get(i));
        }
        return res;
    }
}
```
