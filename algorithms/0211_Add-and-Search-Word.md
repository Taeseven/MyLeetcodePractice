# Implement Trie (Prefix Tree)
------------------
@ [Description](https://leetcode.com/problems/implement-trie-prefix-tree/)  
@ Tags: Backtracking, Design, Trie    
@ Medium

------------------
## Solution
```java
class WordDictionary {
    class Node {
        HashMap<Character, Node> child = new HashMap<>();
        char c;
        boolean isWord;
        public Node() {
            
        }
        
        public Node(char c) {
            this.c = c;
        }
    }
    
    private Node root;
    /** Initialize your data structure here. */
    public WordDictionary() {
        root = new Node();
    }
    
    /** Adds a word into the data structure. */
    public void addWord(String word) {
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
    
    /** Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter. */
    public boolean search(String word) {
        return searchHelper(word, 0, root);
    }
    
    private boolean searchHelper(String word, int index, Node curr) {
        if (index == word.length())
            return curr.isWord;
        char c = word.charAt(index);
        if (c == '.') {
            for (Node node : curr.child.values()) {
                if (searchHelper(word, index + 1, node))
                    return true;
            }
        } if (curr.child.containsKey(c)) {
            return searchHelper(word, index + 1, curr.child.get(c));
        } else {
            return false;
        }
    }
}
```
