# Path Sum IV
------------------
@ [Description](https://leetcode.com/problems/path-sum-iv/)  
@ Tags: Tree  
@ Medium  

------------------
## Solution
数字的前两位可以确定其在书中的位置，可以将数组重新存储在一个map中，通过确定左右子树的位置对应的数字对其进行sum。  
时间及空间复杂度均为$O(N)$  
```java
class Solution {
    int sum = 0;
    HashMap<Integer, Integer> map = new HashMap<>();
    public int pathSum(int[] nums) {
        for (int num : nums) {
            map.put(num / 10, num % 10);
        }
        helper(nums[0]/10 , 0);
        return sum;
    }
    
    private void helper(int key, int currSum) {
        if (map.containsKey(key)) {
            currSum += map.get(key);
            int left = (key / 10 + 1) * 10 + 2 * (key % 10) - 1;
            if (!map.containsKey(left) && !map.containsKey(left + 1))
                sum += currSum;
            helper(left, currSum);
            helper(left + 1, currSum);
        }
    }
}
```
