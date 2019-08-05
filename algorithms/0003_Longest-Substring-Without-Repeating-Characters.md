# Two Sum
------------------
@ [Description](https://leetcode.com/problems/longest-substring-without-repeating-characters/)  
@ Tags: Set, Hash Map  

------------------
> Unique问题可以考虑Set and HashMap

## Solution 1 - Set
利用Set作为Sliding Window，将字符存在Set中。若已存在则将Set最左端的字符移出，左指针右移；若不存在Set中则右指针右移。
* 空间复杂度：$O(min(m, n))$  
* 时间复杂度：$O(n)$ （worst case $\Theta(2N)$)
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Set<Character> set = new HashSet<>();
        int result = 0, right = 0, left = 0;
        while (right < s.length()) {
            if (set.contains(s.charAt(right))) {
                set.remove(s.charAt(left));
                left++;
            } else {
                set.add(s.charAt(right));
                right++;
                result = Math.max(result, right - left);
            }
        }
        return result;
    }
}
```


## Solution 2 - Hash Map
利用HashMap作为Sliding Window，若该字符已存在在Map中则把左边界更新，并将Map值更新,可以跳过使用Set时不断右移左边界的过程。  
* 空间复杂度：$O(min(m, n))$  
* 时间复杂度：$O(n)$

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        HashMap<Character, Integer> map = new HashMap<>();
        int result = 0, leftSide = 0;
        for (int i = 0; i < s.length(); i++) {
            if (map.containsKey(s.charAt(i))) {
                leftSide = Math.max(map.get(s.charAt(i)), leftSide);
            }
            map.put(s.charAt(i), i + 1);
            result = Math.max(result, i - leftSide + 1);   
        }
        return result;
    }
}
```