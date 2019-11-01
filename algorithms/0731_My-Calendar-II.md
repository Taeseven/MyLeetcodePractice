# My Calendar II
------------------
@ [Description](https://leetcode.com/problems/my-calendar-ii/)  
@ Tags: Ordered Map     
@ Medium

------------------
## Solution 1
记录所有的overlap以及所有event，先遍历overlap看是否冲突，再遍历event看是否有新的overlap。  
时间复杂度：$O(N^2)$  
空间复杂度：$O(N)$  
```java
class MyCalendarTwo {
    List<int[]> calendar;
    List<int[]> overlap;

    public MyCalendarTwo() {
        calendar = new ArrayList<>();
        overlap = new ArrayList<>();
    }
    
    public boolean book(int start, int end) {
        for (int[] range : overlap) {
            if (end > range[0] && start < range[1])
                return false;
        }
        for (int[] range : calendar) {
            if (end > range[0] && start < range[1])
                overlap.add(new int[]{Math.max(start,range[0]),Math.min(end,range[1])});
        }
        calendar.add(new int[]{start,end});
        return true;
    }
}
```

## Solution 2
在start的位置+1，end的位置减1.
```java
class MyCalendarTwo {
    TreeMap<Integer, Integer> delta;

    public MyCalendarTwo() {
        delta = new TreeMap();
    }

    public boolean book(int start, int end) {
        delta.put(start, delta.getOrDefault(start, 0) + 1);
        delta.put(end, delta.getOrDefault(end, 0) - 1);

        int active = 0;
        for (int d: delta.values()) {
            active += d;
            if (active >= 3) {
                delta.put(start, delta.get(start) - 1);
                delta.put(end, delta.get(end) + 1);
                if (delta.get(start) == 0)
                    delta.remove(start);
                return false;
            }
        }
        return true;
    }
}
```
