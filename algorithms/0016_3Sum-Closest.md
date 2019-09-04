# 3Sum Closest
------------------
@ [Description](https://leetcode.com/problems/3sum-closest/)  
@ Tags: Array, Pointers  
@ Medium

------------------
## Solution
其思路与 *0015-3Sum* 一致。  
需要注意其输出结果需要一个初始值，但是直接使用MIN_VALUE或MAX_VALUE会出现溢出的情况。  
```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        int res = (target >= 0) ? Integer.MAX_VALUE : Integer.MIN_VALUE;
        int len = nums.length;
        for (int i = 0; i + 2 < len; i++) {
            int l = i + 1, h = len - 1;
            while (l < h) {
                int tmp = nums[i] + nums[h] + nums[l];
                if (tmp == target) return target;
                if (Math.abs(target - res) > Math.abs(target - tmp)) res = tmp;
                if (tmp > target) h--;
                else l++;
            }
        }
        return res;
    }
}
```
