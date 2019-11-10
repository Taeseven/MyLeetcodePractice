# Design Search Autocomplete System
------------------
@ [Description](https://leetcode.com/problems/design-search-autocomplete-system/)  
@ Tags: Design, Trie    
@ Hard

------------------
## Solution
```java
class AutocompleteSystem {
    class TrieNode {
        boolean isWord;
        TrieNode[] next;
        HashMap<String, Integer> map;
        public TrieNode() {
            isWord = false;
            next = new TrieNode[256];
            map = new HashMap<>();
        }
    }
    
    TrieNode root;
    String prefix;
    
    public AutocompleteSystem(String[] sentences, int[] times) {
        root = new TrieNode();
        prefix = "";
        for (int i = 0; i < times.length; i++) {
            insert(sentences[i], times[i]);
        }
    }
    
    private void insert(String sentence, int n) {
        TrieNode curr = root;
        char[] chars = sentence.toCharArray();
        for (char c : chars) {
            TrieNode next = curr.next[c];
            if (next == null) {
                curr.next[c] = new TrieNode();
            }
            curr = curr.next[c];
            curr.map.put(sentence, curr.map.getOrDefault(sentence, 0) + n);
        }
        curr.isWord = true;
    }
    
    public List<String> input(char c) {
//         if finish input
        if (c == '#') {
            insert(prefix, 1);
            prefix = "";
            return new ArrayList<>();
        }
//         get current char
        prefix += c;
        TrieNode curr = root;
        for (char cc : prefix.toCharArray()) {
            TrieNode next = curr.next[cc];
            if (next == null)
                return new ArrayList<>();
            curr = next;
        }
//         autocomplete
        HashMap<String, Integer> count = curr.map;
        PriorityQueue<String> pq = new PriorityQueue<>(new Comparator<String>() {
            public int compare(String i, String j) {
                if (count.get(i) == count.get(j)) {
                    return i.compareTo(j);
                } else return count.get(j) - count.get(i);
            }
        });
        for (String key : count.keySet())
            pq.offer(key);
        List<String> res = new ArrayList<>();
        for (int i = 0; i < 3; i++) {
            if (!pq.isEmpty())
                res.add(pq.poll());
        }
        return res;
    }
}

/**
 * Your AutocompleteSystem object will be instantiated and called as such:
 * AutocompleteSystem obj = new AutocompleteSystem(sentences, times);
 * List<String> param_1 = obj.input(c);
 */
```
