# Longest Consecutive Sequence
------------------
@ [Description](https://leetcode.com/problems/longest-consecutive-sequence/)  
@ Tags: Array, Union Find    
@ Hard

------------------
## Solution 1 - Sort
时间复杂度：$O(NlogN)$  
空间复杂度：$O(N)$  
```java
class Solution {
    public int longestConsecutive(int[] nums) {
        if (nums.length == 0)
            return 0;
        Arrays.sort(nums);
        int max = 1, curr = 1;
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] == nums[i-1])
                continue;
            if (nums[i] == nums[i-1] + 1)
                curr++;
            else {
                max = Math.max(max, curr);
                curr = 1;
            }
        }
        return Math.max(max, curr);
    }
}
```

## Solution 2 - Hash Set
HashSet可以帮助快速lookup。  
首先将数存入set中，然后若num-1不在set中则表明其是序列的起点，那么不过验证set中是否包含下一位即可。  
时间复杂度：$O(N)$  
空间复杂度：$O(N)$ 
```java
class Solution {
    public int longestConsecutive(int[] nums) {
        if (nums.length == 0)
            return 0;
        Set<Integer> set = new HashSet<>();
        for (int num : nums)
            set.add(num);
        int max = 0;
        for (int num : set) {
            if (!set.contains(num - 1)) {
                int curr_num = num;
                int curr = 1;
                while (set.contains(curr_num + 1)) {
                    curr_num++;
                    curr++;
                }
                max = Math.max(max, curr);
            }
        }
        return max;
    }
}
```
