# Sort Colors
------------------
@ [Description](https://leetcode.com/problems/sort-colors/)  
@ Tags: Array, Two Pointers, Sort     
@ Medium

------------------
## Solution 1 - Two Pass
第一遍统计出现的次数，第二遍进行in-place更新值。  
```java
class Solution {
    public void sortColors(int[] nums) {
        int count_0 = 0, count_1 = 0, count_2 = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == 0) count_0++;
            else if (nums[i] == 1) count_1++;
            else count_2++;
        }
        for (int i = 0; i < nums.length; i++) {
            if (i < count_0) nums[i] = 0;
            else if (i >= count_0 && i < count_0 + count_1) nums[i] = 1;
            else nums[i] = 2;
        }
    }
}
```
Follow Up: 如何只用One-Pass(Solution 2)

## Solution 2 - One Pass
两个指针记录’0‘的尾巴和’2‘的头即可。  
注意swap 0时，curr一定要更新。
```java
class Solution {
    public void sortColors(int[] nums) {
        if (nums.length == 0 || nums.length == 1)
            return;
        int p0 = 0, curr = 0;
        int p2 = nums.length - 1;
        int tmp;
        while (curr <= p2) {
            if (nums[curr] == 2) {
                tmp = nums[curr];
                nums[curr] = nums[p2];
                nums[p2--] = tmp;
            } else if (nums[curr] == 0) {
                tmp = nums[curr];
                nums[curr++] = nums[p0];
                nums[p0++] = tmp;
            } else curr++;
        }
    }
}
```
Follow Up: In-place sort algorithm
