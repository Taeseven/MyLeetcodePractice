# Maximum Average Subtree
@ [Description](https://leetcode.com/problems/maximum-average-subtree/)  
@ Tags: Tree        
@ Medium

------------------
## Solution 1
定义一个新class储存子树的sum和count，遍历该树以得到最大均值的子树。  
```java
class Solution {
    double max = 0.0;
    
    class returnType {
        int sum;
        int count;
        returnType (int sum, int count) {
            this.sum = sum;
            this.count = count;
        }
    }
    
    public double maximumAverageSubtree(TreeNode root) {
        helper(root);
        return max;
    }
    
    private returnType helper(TreeNode root) {
        if (root == null) {
            return new returnType(0, 0);
        }
        if (root.right == null && root.left == null) {
            max = (root.val > max) ? root.val : max;
            return new returnType(root.val, 1);
        }
        returnType left = helper(root.left);
        returnType right = helper(root.right);
        
        int sum = left.sum + right.sum + root.val;
        int count = left.count  + right.count + 1;
        
        if ((double) sum / count > max)
            max = (double) sum/count;

        return new returnType(sum, count);
        
    }
}
```
