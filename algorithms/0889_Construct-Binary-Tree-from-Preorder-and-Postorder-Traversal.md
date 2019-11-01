# Construct Binary Tree from Preorder and Postorder Traversal
------------------
@ [Description](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-postorder-traversal/)  
@ Tags: Tree     
@ Medium

------------------
## Solution
现有一个tree = [1,2,3,4,5,6,7]  
pre = [1,2,4,5,3,6,7]  
post = [4,5,2,6,7,3,1]  

根据规律我们可以发现pre第一位和post最后一位是root。  
当在post遍历到“2”时，post的前部分就构成了根的左子树，后半部为右字数。  

时间复杂度：$O(NlogN) \~ O(N^2)$  
空间复杂度：$O(logN) \~ O(N)$  

```java
class Solution {
    int[] pre;
    int[] post;
    public TreeNode constructFromPrePost(int[] pre, int[] post) {
        this.pre = pre;
        this.post = post;
        return helper(0,0,pre.length);
    }
    
    private TreeNode helper(int i, int j, int n) {
        if (n <= 0)
            return null;
        if (n == 1)
            return new TreeNode(pre[i]);
        TreeNode root = new TreeNode(pre[i]);
        int k = j;
        while (pre[i + 1] != post[k]) k++;
        int l = k - j + 1;
        root.left = helper(i + 1, j, l);
        root.right = helper(i + l + 1, k + 1, n - l - 1);
        return root;
    }
}
```

可以通过hashtable储存pre与post位置的对应关系，将时间复杂度降为O(N).  
```java
class Solution {
    Map<Integer, Integer> map;
    int[] pre;
    int[] post;
    
    public TreeNode constructFromPrePost(int[] pre, int[] post) {
        map = new HashMap<>();
        this.pre = pre;
        this.post = post;
        for (int i = 0; i < post.length; i++) 
            map.put(post[i], i);
        return helper(0, 0, pre.length);
    }
    
    private TreeNode helper(int i, int j, int n) {
        if (n <= 0)
            return null;
        if (n == 1)
            return new TreeNode(pre[i]);
        TreeNode root = new TreeNode(pre[i]);
        int k = map.get(pre[i + 1]);
        int l = k - j + 1;
        root.left = helper(i + 1, j, l);
        root.right = helper(i + l + 1, k + 1, n - l - 1);
        return root;
    }
}
```
