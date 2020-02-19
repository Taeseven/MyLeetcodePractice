# Implement Trie (Prefix Tree)
------------------
@ [Description](https://leetcode.com/problems/implement-trie-prefix-tree/)  
@ Tags: Design, Trie    
@ Medium

------------------
## Solution
Trie时间复杂度和hashmap其实是一样的，空间上利用hashmap可以优于hashmap。  
```java
class Trie {
    class Node {
        HashMap<Character, Node> child = new HashMap<>();
        boolean isWord;
        char c;
        public Node(char c) {
            this.c = c;
        }
        
        public Node() {
            
        }
    }
    
    private Node root;
    
    /** Initialize your data structure here. */
    public Trie() {
        root = new Node();
    }
    
    /** Inserts a word into the trie. */
    public void insert(String word) {
        Node curr = root;
        for (Character c : word.toCharArray()) {
            if (curr.child.containsKey(c)) {
                curr = curr.child.get(c);
            } else {
                Node newNode = new Node(c);
                curr.child.put(c, newNode);
                curr = newNode;
            }
        }
        curr.isWord = true;
    }
    
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        Node res = searchHelper(word);
        if (res == null)
            return false;
        return res.isWord;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        return searchHelper(prefix) != null;
    }
    
    private Node searchHelper(String word) {
        Node curr = root;
        for (Character c : word.toCharArray()) {
            if (curr.child.containsKey(c)) {
                curr = curr.child.get(c);
            } else {
                return null;
            }
        }
        return curr;
    }
}
```
