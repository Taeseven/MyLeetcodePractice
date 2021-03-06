# Majority Element
------------------
@ [Description](https://leetcode.com/problems/majority-element/)  
@ Tags: Array, Divide and Conquer, Bit Manipulation   
@ Easy

------------------
## Solution 1 - Divide and Conquer
时间复杂度：$O(NlogN)$  
空间复杂度：$O(N)$  
```java
class Solution {
    private int countInRange(int[] nums, int num, int lo, int hi) {
        int count = 0;
        for (int i = lo; i <= hi; i++) {
            if (nums[i] == num) {
                count++;
            }
        }
        return count;
    }

    private int majorityElementRec(int[] nums, int lo, int hi) {
        // base case; the only element in an array of size 1 is the majority
        // element.
        if (lo == hi) {
            return nums[lo];
        }

        // recurse on left and right halves of this slice.
        int mid = (hi-lo)/2 + lo;
        int left = majorityElementRec(nums, lo, mid);
        int right = majorityElementRec(nums, mid+1, hi);

        // if the two halves agree on the majority element, return it.
        if (left == right) {
            return left;
        }

        // otherwise, count each element and return the "winner".
        int leftCount = countInRange(nums, left, lo, hi);
        int rightCount = countInRange(nums, right, lo, hi);

        return leftCount > rightCount ? left : right;
    }

    public int majorityElement(int[] nums) {
        return majorityElementRec(nums, 0, nums.length-1);
    }
}
```

## Solution 2 -Boyer-Moore Algorithm
时间复杂度：$O(N)$  
空间复杂度：$O(1)$  
```java
class Solution {
    public int majorityElement(int[] nums) {
        int count = 0;
        Integer x = null;
        for (int num : nums) {
            if (count == 0)
                x = num;
            count += (x == num) ? 1 : -1;
        }
        return x;
    }
}
```
