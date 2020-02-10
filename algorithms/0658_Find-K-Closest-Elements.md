# Find K Closest Elements
------------------
@ [Description](https://leetcode.com/problems/find-k-closest-elements/)  
@ Tags: Binary Search    
@ Medium

------------------
## Solution 1 - Priority Queue
需要改写priority queue的comparator。  
时间复杂度：$O(NlogN)$  
空间复杂度：$O(N)$  
```java
class Solution {
    public List<Integer> findClosestElements(int[] arr, int k, int x) {
        PriorityQueue<Integer> pq = new PriorityQueue<>(new Comparator<Integer>() {
            public int compare(Integer i, Integer j) {
                if (Math.abs(i - x) == Math.abs(j - x))
                    return j - i;
                return Math.abs(j - x) - Math.abs(i - x);
            }
        });
        List<Integer> res = new ArrayList<>();
        for (int num : arr) {
            pq.offer(num);
            if (pq.size() > k)
                pq.poll();
        }
        while (!pq.isEmpty())
            res.add(pq.poll());
        Collections.sort(res);
        return res;
    }
}
```

## Solution 2 - Binary Search
利用mid作为interval的起点，mid+k为终点进行判断。  
时间复杂度：$O(logN)$  
```java
class Solution {
    public List<Integer> findClosestElements(int[] arr, int k, int x) {
        int left = 0, right = arr.length - k;
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (x - arr[mid] > arr[mid + k] - x)
                left = mid + 1;
            else
                right = mid;
        }
        List<Integer> res = new ArrayList<>();
        for (int i = left; i < left + k; i++)
            res.add(arr[i]);
        return res;
    }
}
```
