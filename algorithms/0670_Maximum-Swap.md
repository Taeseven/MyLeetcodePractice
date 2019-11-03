# Maximum Swap
------------------
@ [Description](https://leetcode.com/problems/maximum-swap/)  
@ Tags: Array, Math    
@ Medium

------------------
## Solution
遍历一边，记录每个数字出现的最后index。  
再从头查找比当前数字大的数字（从大到小），他们最后一次出现的位置是否在当前数字后面，若是则进行swap输出即可。  
```java
class Solution {
    public int maximumSwap(int num) {
        char[] nums = Integer.toString(num).toCharArray();
        int[] index = new int[10];
        for (int i = 0; i < nums.length; i++)
            index[nums[i] - '0'] = i;
        for (int i = 0; i < nums.length; i++) {
            for (int d = 9; d > nums[i] - '0'; d--) {
                if (index[d] > i) {
                    char tmp = nums[i];
                    nums[i] = nums[index[d]];
                    nums[index[d]] = tmp;
                    return Integer.valueOf(new String(nums));
                }
            }
        }
        return num;
    }
}
```
