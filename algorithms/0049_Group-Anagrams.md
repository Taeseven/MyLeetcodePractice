# Group Anagrams
------------------
@ [Description](https://leetcode.com/problems/group-anagrams//)  
@ Tags: HashTable, String    
@ Medium

------------------
## Solution
可以将string转变成为array再对其sort，因此不同的组合都会有唯一的key。  
时间复杂度：$O(NKlogK)$  
空间复杂度：$O(NK)$
```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        if (strs.length == 0)
            return new ArrayList<>();
        Map<String, List> map = new HashMap<>();
        for (String s : strs) {
            char[] c = s.toCharArray();
            Arrays.sort(c);
            String key = String.valueOf(c);
            if (!map.containsKey(key))
                map.put(key, new ArrayList<>());
            map.get(key).add(s);
        }
        return new ArrayList(map.values());
    }
}
```
也可以考虑用count数组当做key，未出现的字符可以特殊处理以降低时间复杂度。
