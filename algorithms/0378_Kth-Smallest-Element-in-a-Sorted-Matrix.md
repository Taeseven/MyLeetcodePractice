#  Kth Smallest Element in a Sorted Matrix
------------------
@ [Description](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/)  
@ Tags: Binary Search, Heap    
@ Medium

------------------
## Solution 1 - Max Heap
时间复杂度：$O(Nlogk)$  
空间复杂度：$O(N)$  
```java
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        PriorityQueue<Integer> pq = new PriorityQueue<>((a, b) -> (b - a));
        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix.length; j++) {
                pq.offer(matrix[i][j]);
                if (pq.size() > k)
                    pq.poll();
            }
        }
        return pq.poll();
    }
}
```

## Solution 2 - Binary Search
The correctness of this algorithm is to ensure that the target value is within the range of [low, high] for each loop step.  
For example, there is a matrix and the k = 14,  
[11, 15, 20, 21]  
[12, 16, 25, 26]  
[16, 20, 30, 31]  
[30, 31, 35, 38]  
It is easy to find the target value is 31, and the algorithm will make sure the target value is within the range of [low, high].  
First step, let low = 11, high = 38, and target value must in the range of [11, 38], so mid is 24, count = 8, count < k, let low = 24 + 1 = 25, now target value 31 is within the range of [25, 38].  
Second step, low = 25, high = 38, mid = 31, count = 14, count = k, let high = mid = 31, now target value 31 is also within the range of [25, 31].  
Third step, low = 25, high = 31, mid = 28, count = 10, count < k, let low = mid + 1 = 29, now target value 31 is also within the range of [29, 31].  
Next step, low = 29, high = 31, mid = 30, count = 12, count < k, let low = mid + 1 = 31, now target value 31 is also within the range of [31, 31]. Now low == high, we find the target value.  
Notice that every time the algorithm narrows the range, the target value must in the new range. When count >= k, the mid is big enough, the target value must in the range of [low, mid], so let high = mid. When count < k, the mid is small, the target value must in the range of [mid+1, high], so let low = mid + 1. This loop invariants will remain until the algorithm gets end (low == high).  
```java
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        int m = matrix.length, n = matrix[0].length;
        int low = matrix[0][0], high = matrix[m-1][n-1];
        while (low < high) {
            int mid = low + (high - low) / 2;
            int count = 0;
            for (int i = 0; i < m; i++) {
                int j = n - 1;
                while (j >= 0 && matrix[i][j] > mid) 
                    j--;
                count += j + 1;
            }
            if (count < k)
                low = mid + 1;
            else
                high = mid;
        }
        return low;
    }
}
```
