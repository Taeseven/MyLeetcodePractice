#  Find Anagram Mappings
------------------
@ [Description](https://leetcode.com/problems/find-anagram-mappings/)  
@ Tags: HashTable    
@ Easy

------------------
## Solution
需要考虑重复的情况，所以hashmap的value应当是个list。  
```java
class Solution {
    public int[] anagramMappings(int[] A, int[] B) {
        int[] res = new int[A.length];
        Map<Integer, List<Integer>> map = new HashMap<>();
        for (int i = 0; i < B.length; i++) {
            List tmp = map.getOrDefault(B[i], new ArrayList<>());
            tmp.add(i);
            map.put(B[i], tmp);
        }
        for (int i = 0; i < A.length; i++) {
            res[i] = map.get(A[i]).get(0);
        }
        return res;
    }
}
```
