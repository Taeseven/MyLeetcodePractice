#  Top K Frequent Elements
------------------
@ [Description](https://leetcode.com/problems/top-k-frequent-elements/)  
@ Tags: Hash Table, Heap     
@ Medium

------------------
## Solution - Hash Table + Heap
时间复杂度：$O(N) + O(Nlog(k)) = O(Nlog(k))$
空间复杂度：$O(N)$  
```java
class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        HashMap<Integer, Integer> count = new HashMap<>();
        for (int n : nums)
            count.put(n, count.getOrDefault(n, 0) + 1);
        PriorityQueue<Integer> heap = new PriorityQueue<Integer>((n1, n2) -> count.get(n1) - count.get(n2));
        for (int n : count.keySet()) {
            heap.add(n);
            if (heap.size() > k)
                heap.poll();
        }
        List<Integer> res = new LinkedList<>();
        while (!heap.isEmpty())
            res.add(heap.poll());
        Collections.reverse(res);
        return res;
    }
}
```

## Solution 2 - Hash Table + Bucket
时间复杂度：$O(N)$   
空间复杂度：$O(N)$ 
```java
class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        HashMap<Integer, Integer> count = new HashMap<>();
        for (int n : nums)
            count.put(n, count.getOrDefault(n, 0) + 1);
        List<Integer> res = new LinkedList<>();
        LinkedList<Integer>[] buckets = new LinkedList[nums.length + 1];
        for (int n : count.keySet()) {
            int freq = count.get(n);
            if (buckets[freq] == null)
                buckets[freq] = new LinkedList<>();
            buckets[freq].add(n);
        }
        int idx = nums.length;
        for (int i = 0; i < k; i++) {
            while (buckets[idx] == null || buckets[idx].size() == 0)
                idx--;
            res.add(buckets[idx].remove());
        }
        return res;
    }
}
```