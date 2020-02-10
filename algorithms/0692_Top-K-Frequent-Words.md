# Top K Frequent Words
------------------
@ [Description](https://leetcode.com/problems/top-k-frequent-words/)  
@ Tags: Hash Table, Heap, Trie    
@ Medium

------------------
## Solution
时间复杂度：$O(NlogK)$   
空间复杂度：$O(N)$ 
```java
class Solution {
    public List<String> topKFrequent(String[] words, int k) {
        HashMap<String, Integer> map = new HashMap<>();
        PriorityQueue<String> pq = new PriorityQueue(new Comparator<String> () {
            public int compare(String i, String j) {
                if (map.get(i) == map.get(j))
                    return j.compareTo(i);
                return map.get(i) - map.get(j);
            }
        });
        for (String s : words)
            map.put(s, map.getOrDefault(s, 0) + 1);
        for (String s : map.keySet()) {
            pq.offer(s);
            if (pq.size() > k)
                pq.poll();
        }
        List<String> res = new ArrayList<>();
        while (!pq.isEmpty())
            res.add(pq.poll());
        Collections.reverse(res);
        return res;
    }
}
```
