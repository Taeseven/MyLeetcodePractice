#  Meeting Rooms II
------------------
@ [Description](https://leetcode.com/problems/meeting-rooms-ii/)  
@ Tags: Heap, Greedy, Sort     
@ Medium

------------------
## Solution - Sort
```java
class Solution {
    public int minMeetingRooms(int[][] intervals) {
        if (intervals == null || intervals.length == 0 || intervals[0].length == 0)
            return 0;
        int[] start = new int[intervals.length];
        int[] end = new int[intervals.length];
        for (int i = 0; i < intervals.length; i++) {
            start[i] = intervals[i][0];
            end[i] = intervals[i][1];
        }
        int end_index = 0;
        int res = 1;
        Arrays.sort(start);
        Arrays.sort(end);
        for (int i = 1; i < intervals.length; i++) {
            if (start[i] < end[end_index]) {
                res = Math.max(i - end_index + 1, res);
            } else end_index++;
        }
        return res;
    }
}
```
