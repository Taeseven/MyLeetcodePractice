# Binary Search Tree Iterator
------------------
@ [Description](https://leetcode.com/problems/binary-search-tree-iterator/)  
@ Tags: Stack, Tree, Design  
@ Medium

------------------
## Solution 1 - InOrder
时间和空间复杂度都是$O(N)$, next()和hasNext()都是$O(1)$.  
```java
class BSTIterator {
    List<Integer> values = new ArrayList<>();
    int index = 0;

    public BSTIterator(TreeNode root) {
        inOrder(root);       
    }
    
    private void inOrder(TreeNode root) {
        if (root == null)
            return;
        inOrder(root.left);
        values.add(root.val);
        inOrder(root.right);
    }
    
    /** @return the next smallest number */
    public int next() {
        return values.get(index++);
    }
    
    /** @return whether we have a next smallest number */
    public boolean hasNext() {
        return index < values.size();
    }
}
```

## Solution 2 - Stack
空间复杂度为$O(h)$.  
```java
class BSTIterator {
    Stack<TreeNode> stack = new Stack<>();
    public BSTIterator(TreeNode root) {
        while (root != null) {
            stack.push(root);
            root = root.left;
        }
    }
    
    /** @return the next smallest number */
    public int next() {
        TreeNode tmp = stack.pop();
        if (tmp.right != null) {
            while (tmp.right != null) {
                stack.push(tmp.right);
                tmp.right = tmp.right.left;
            }
        }
        return tmp.val;
    }
    
    /** @return whether we have a next smallest number */
    public boolean hasNext() {
        return !stack.isEmpty();
    }
}
```

