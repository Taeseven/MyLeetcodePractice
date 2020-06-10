# Partition Labels
------------------
@ [Description](https://leetcode.com/problems/partition-labels/)  
@ Tags: Two Pointer, Greedy   
@ Medium

------------------
## Solution
首先得到每个字符最后一次出现的位置。然后利用两个指针start和end表示当前子字符串的起止点，遍历整个字符串。如果当前字符最后一次出现的位置大于终止指针，那么就更新终止指针。知道终止指针去当前字符的index一致时，代表子字符串满足条件，将其写出返回的列表中，然后更新起始指针即可。  
时间复杂度$O(n)$  
空间复杂度$O(1)$  
```java
class Solution {
    public List<Integer> partitionLabels(String S) {
        int[] last_index = new int[26];
        // get index of the last char x
        for (int i = 0; i < S.length(); i++) {
            last_index[S.charAt(i) - 'a'] = i;
        }
        
        List<Integer> res = new ArrayList<>();
        int start = 0, end = 0;
        for (int i = 0; i < S.length(); i++) {
            end = Math.max(end, last_index[S.charAt(i) - 'a']);
            if (i == end) {
                res.add(end - start + 1);
                start = end + 1;
            }
        }
        return res;
    }
}
```
