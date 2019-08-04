# Two Sum
------------------
@ [Description](https://leetcode.com/problems/two-sum/)  
@ Tags: Arrays, Hash Table  

------------------
## Solution 1 - Brute Force  
暴力解决，循环遍历输入两次  
时间复杂度$O(n^2)$， 空间复杂度$O(1)$  
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[i] + nums[j] == target) {
                    return new int[]{i, j};
                }
            }
        }
        return null;
    }
}
```

------------------
## Solution 2 - Hash Table 
利用Hash Table，每次将当前值与target的差值及其index存在Map中，当遍历其他元素时若Map中已存在当前值则可直接输出。  
时间及空间复杂度均为$O(n)$  
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> remainder = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            if (!remainder.containsKey(nums[i])) {
                remainder.put(target - nums[i], i);
            } else {
                return new int[]{remainder.get(nums[i]), i};
            }    
        }
        return null;
    }
}
```

