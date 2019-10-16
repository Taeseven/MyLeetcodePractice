#  Word Ladder
------------------
@ [Description](https://leetcode.com/problems/word-ladder/)  
@ Tags: BFS   
@ Hard

------------------
## Solution - BFS
利用BFS进行搜索，注意为了程序运行速度以及空间，可以删除已访问过的word，同时在计算前先用set去除重复的word.  
空间复杂度：$O(MN)$ M是word长度  
时间复杂度：$O(MN)$  
```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        if (wordList == null || wordList.size() == 0 || beginWord == endWord)
            return 0;
        Set<String> words = new HashSet<>(wordList);
        Queue<String> queue = new LinkedList<>();
        queue.offer(beginWord);
        int len = 1;
        while (!queue.isEmpty()) {
            int size = queue.size();
            len++;
            for (int j = 0; j < size; j++) {
                String cur = queue.poll();
                char[] curr = cur.toCharArray();
                for (int i = 0; i < curr.length; i++) {
                    for (char c = 'a'; c <= 'z'; c++) {
                        if (c == curr[i])
                            continue;
                        char tmp = curr[i];
                        curr[i] = c;
                        String next = new String(curr);
                        if (words.contains(next)) {
                            if (next.equals(endWord))
                                return len;
                            queue.offer(next);
                            words.remove(next);
                        }     
                        curr[i] = tmp;
                    }
                }
            }
        }
        return 0;
    }
}
```
优化：可以从start及end同时向中间搜索。
