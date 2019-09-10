# Next Permutation
------------------
@ [Description](https://leetcode.com/problems/next-permutation/)  
@ Tags: Array   
@ Medium

------------------
 # Solution
找到变换的规律。需要将从末尾开始第一个违背nums[i]>=nums[i+1]的数字与其从末尾开始第一个小于它的数字进行交换，并将i+1后的数字全部reverse。
时间复杂度：$O(n)$
```java
class Solution {
    public void nextPermutation(int[] nums) {
        int i = nums.length - 2;
        while (i >= 0 && nums[i] >= nums[i + 1]) i--;
        if (i >= 0) {
            int j = nums.length - 1;
            while (j > i && nums[i] >= nums[j]) j--;
            swap(nums, i, j);
        }
        reverse(nums, i+1);
    }
    
    private void swap(int[] nums, int i , int j) {
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
    
    private void reverse(int[] nums, int start) {
        int end = nums.length - 1;
        while (end > start) {
            swap(nums, start, end);
            start++;
            end--;
        }
    }
}
```
