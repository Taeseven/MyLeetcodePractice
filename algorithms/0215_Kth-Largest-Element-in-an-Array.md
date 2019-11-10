# Kth Largest Element in an Array
------------------
@ [Description](https://leetcode.com/problems/kth-largest-element-in-an-array/)  
@ Tags: Divide and Conquer, Heap    
@ Medium

------------------
## Solution 1 - Min Headp
时间复杂度：$O(Nlogk)$  
空间复杂度：$O(k)$  
```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        if (nums == null || nums.length == 0 || k > nums.length)
            return -1;
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        for (int num : nums) {
            pq.offer(num);
            if (pq.size() > k)
                pq.poll();
        }
        return pq.poll();
    }
}
```

## Solution 2 - Max Heap
需要重新写Comparator。  
时间复杂度：$O(NlogN)$  
空间复杂度：$O(N)$
```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        if (nums == null || nums.length == 0 || k > nums.length)
            return -1;
        PriorityQueue<Integer> pq = new PriorityQueue<>(new Comparator<Integer>() {
            public int compare(Integer i, Integer j) {
                if (i == j) return 0;
                if (i > j) return -1;
                else return 1;
            }
        });
        for (int num : nums)
            pq.offer(num);
        for (int i = 0; i < k - 1; i++)
            pq.poll();
        return pq.poll();
    }
}
```

## Solution 3 - Quick Select
时间复杂度：$O(N)$  
空间复杂度：$O(1)$
```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        if (nums == null || nums.length == 0 || k > nums.length)
            return -1;
        int low = 0;
        int high = nums.length - 1;
        while (true) {
            int pos = partition(nums, low, high);
            if (pos == k - 1) 
                return nums[pos];
            if (pos < k)
                low = pos + 1;
            else
                high = pos - 1;
        }
    }
    private int partition(int[] nums, int low, int high) {
        int p = low;
        for (int i = low; i <= high; i++) {
            if (nums[i] > nums[high]) {
                int tmp = nums[p];
                nums[p] = nums[i];
                nums[i] = tmp;
                p++;
            }
        }
        int tmp = nums[p];
        nums[p] = nums[high];
        nums[high] = tmp;
        return p;
    }
}
```
