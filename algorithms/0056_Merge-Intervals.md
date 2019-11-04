# Merge Intervals
------------------
@ [Description](https://leetcode.com/problems/merge-intervals/)  
@ Tags: Array, sort     
@ Medium

------------------
## Solution
先将input根据开始时间sort，然后遍历如果新的时间开始时间在旧的区间内则更新旧区间的end，反之则将当前区间赋值给旧的区间。  
```java
class Solution {
    public int[][] merge(int[][] intervals) {
        if (intervals == null || intervals.length == 0 || intervals[0].length == 0)
            return new int[0][];
        Arrays.sort(intervals, (a, b) -> (a[0] - b[0]));
        int i = 0;
        List<int[]> list = new ArrayList<>();
        int[] last = intervals[0];
        while (i < intervals.length) {
            if (intervals[i][0] <= last[1])
                last[1] = Math.max(last[1], intervals[i][1]);
            else {
                list.add(last);
                last = intervals[i];
            }
            i++;
        }
        list.add(last);
        return list.toArray(new int[list.size()][]);
    }
}
```
