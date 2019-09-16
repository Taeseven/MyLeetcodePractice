# Two Sum II - Input array is sorted
@ [Description](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)  
@ Tags: Array, Two Pointers, Binary Search  
@ Easy

------------------
## Solution
```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int low = 0, high = numbers.length - 1;
        while (low < high) {
            if (numbers[low] + numbers[high] == target) {
                return new int[]{low + 1, high + 1};
            } else {
                if (numbers[low] + numbers[high] > target) high--;
                else low++;
            }
        }
        return new int[]{-1, -1};
    }
}
```
