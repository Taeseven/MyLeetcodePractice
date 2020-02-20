# Prefix and Suffix Search
------------------
@ [Description](https://leetcode.com/problems/prefix-and-suffix-search/)  
@ Tags: Trie    
@ Hard

------------------
## Solution 1 - Two Tries
利用两个Trie分别按照suffix和prefix的顺序存word，利用两个set求交集。但是时间和空间复杂度较高。  
```java
class WordFilter {
    class Trie {
        HashMap<Character, Trie> child = new HashMap<>();
        char c;
        Set<String> words;
        public Trie() {
            words = new HashSet<>();
        }
        public Trie(char c) {
            this.c = c;
            words = new HashSet<>();
        }
    }
    private Trie root1;
    private Trie root2;
    public WordFilter(String[] words) {
        root1 = new Trie();
        root2 = new Trie();
        for (String word : words) {
            Trie curr = root1;
            for (Character c : word.toCharArray()) {
                if (curr.child.containsKey(c)) {
                    curr = curr.child.get(c);
                } else {
                    Trie newNode = new Trie(c);
                    curr.child.put(c, newNode);
                    curr = newNode;
                }
                curr.words.add(word);
            }
            curr = root2;
            for (int i = word.length() - 1; i >= 0; i--) {
                if (curr.child.containsKey(word.charAt(i))) {
                    curr = curr.child.get(word.charAt(i));
                } else {
                    Trie newNode = new Trie(word.charAt(i));
                    curr.child.put(word.charAt(i), newNode);
                    curr = newNode;
                }
                curr.words.add(word);
            }
        }
    }
    
    public int f(String prefix, String suffix) {
        Set preSet = search(prefix, true);
        Set sufSet = search(suffix, false);
        if (preSet.size() == 0 || sufSet.size() == 0)
            return -1;
        for (Object word : preSet) {
            if (sufSet.contains((String) word))
                return 0;
        }
        return -1;
    }
    
    private Set<String> search(String fix, boolean flag) {
        Trie curr;
        if (flag) 
            curr = root1;
        else
            curr = root2;
        for (Character c : fix.toCharArray()) {
            if (curr.child.containsKey(c)) {
                curr = curr.child.get(c);
            } else {
                return null;
            }
        }
        return curr.words;
    }
    
}
```

## Solution 2 
重新整理下要存储的word，即将其改为suffix + ‘.' + prefix 的结构，也就是说一个词要根据不同的pre和suf的组合储存多次。  
（其实感觉空间和时间上也很复杂...，不懂为什么这个方法更好）  
```java
class WordFilter {
    class Trie {
        HashMap<Character, Trie> child = new HashMap<>();
        char c;
        int weight = 0;
        public Trie() {
        }
        public Trie(char c) {
            this.c = c;
        }
    }
    private Trie root;
    public WordFilter(String[] words) {
        root = new Trie();
        for (int weight =0; weight < words.length; weight++) {
            String tmp = words[weight] + ".";
            for (int i = 0; i < tmp.length(); i++) {
                Trie curr = root;
                // curr.weight = weight;
                for (int j = i; j < 2 * tmp.length() - 1; j++) {
                    char c = tmp.charAt(j % tmp.length());
                    if (curr.child.containsKey(c)) {
                        curr = curr.child.get(c);
                    } else {
                        Trie newNode = new Trie(c);
                        curr.child.put(c, newNode);
                        curr = newNode;
                    }
                    curr.weight = weight;
                }
            }
        }
    }
    
    public int f(String prefix, String suffix) {
        Trie curr = root;
        String tmp = suffix + '.' + prefix;
        for (Character c : tmp.toCharArray()) {
            if (!curr.child.containsKey(c))
                return -1;
            curr = curr.child.get(c);
        }
        return curr.weight;
    }
}

/**
 * Your WordFilter object will be instantiated and called as such:
 * WordFilter obj = new WordFilter(words);
 * int param_1 = obj.f(prefix,suffix);
 */
 ```
 