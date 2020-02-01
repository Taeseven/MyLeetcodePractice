#  Find Smallest Letter Greater Than Target
------------------
@ [Description](https://leetcode.com/problems/find-smallest-letter-greater-than-target/)  
@ Tags: Binary Search    
@ Easy

------------------
## Solution
时间复杂度：$O(logN)$
```java
class Solution {
    public char nextGreatestLetter(char[] letters, char target) {
        int l = 0, r = letters.length;
        while (l < r) {
            int mid = l + (r - l) / 2;
            if (letters[mid] <= target)
                l = mid + 1;
            else
                r = mid;
        }
        return letters[l % letters.length];
    }
}
```
