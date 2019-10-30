# My Calendar I
------------------
@ [Description](https://leetcode.com/problems/my-calendar-i/)  
@ Tags: Array     
@ Medium

------------------
## Solution 1 - Array
时间复杂度 $O(N^2)$  
空间复杂度 $O(N)$
```java
class MyCalendar {
    List<int[]> calendar;
    public MyCalendar() {
        calendar = new ArrayList<>();
    }
    
    public boolean book(int start, int end) {
        for (int[] time : calendar) {
            if (time[0] < end && time[1] > start)
                return false;
        }
        calendar.add(new int[]{start, end});
        return true;
    }
}
```

## Solution 2 - TreeMap
时间复杂度 $O(NlogN)$  
空间复杂度 $O(N)$  
> - TreeMap.floorKey(start): return the largest key <= start;
> - TreeMap.ceilingKey(start): return the smallest key >= start;
```java
class MyCalendar {
    TreeMap<Integer, Integer> calendar;
    public MyCalendar() {
        calendar = new TreeMap();
    }
    
    public boolean book(int start, int end) {
        Integer prev = calendar.floorKey(start);
        Integer next = calendar.ceilingKey(start);
        if ((prev == null || calendar.get(prev) <= start) &&
           (next == null || end <= next)) {
            calendar.put(start, end);
            return true;
        }
        return false;
    }
}
```