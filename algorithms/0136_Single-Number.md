# Single Number
------------------
@ [Description](https://leetcode.com/problems/single-number/)  
@ Tags: Hash Table, Bit Manipulation   
@ East

------------------
## Solution 1 - HashMap
时间和空间复杂度：$O(N)$
```java
class Solution {
    public int singleNumber(int[] nums) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int num : nums) {
            if (map.containsKey(num))
                map.remove(num);
            else
                map.put(num, 1);
        }
        return (int) map.keySet().toArray()[0];
    }
}
```

## Solution 2 - XOR
存在相同两个数字的话，异或的结果为0  
空间复杂度为$O(1)$  
```java
class Solution {
    public int singleNumber(int[] nums) {
        int res = 0;
        for (int num : nums)
            res ^= num;
        return res;
    }
}
```
