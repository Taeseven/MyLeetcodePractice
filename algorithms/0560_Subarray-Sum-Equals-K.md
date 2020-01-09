# Subarray Sum Equals K
------------------
@ [Description](https://leetcode.com/problems/subarray-sum-equals-k/)  
@ Tags: Array, Hash Table  
@ Medium

------------------
## Solution
用一个hash table储存所有presum值及个数。  
时间空间复杂度均为$O(N)$  
```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        HashMap<Integer, Integer> map = new HashMap<>();
        int count = 0, sum = 0;
        map.put(0, 1);
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            if (map.containsKey(sum - k))
                count += map.get(sum - k);
            map.put(sum, map.getOrDefault(sum, 0) + 1);
        }
        return count;
    }
}
```
