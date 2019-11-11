# My Calendar III
------------------
@ [Description](https://leetcode.com/problems/my-calendar-ii/)  
@ Tags: Ordered Map, Segment Tree     
@ Hard

------------------
## Solution - TreeMap
```java
class MyCalendarThree {
    TreeMap<Integer, Integer> calendar;

    public MyCalendarThree() {
        calendar = new TreeMap<>();
    }
    
    public int book(int start, int end) {
        calendar.put(start, calendar.getOrDefault(start, 0) + 1);
        calendar.put(end, calendar.getOrDefault(end, 0) - 1);
        int count = 0;
        int max = 0;
        for (int v : calendar.values()) {
            count += v;
            max = Math.max(max, count);
        }
        return max;
    }
}
```
