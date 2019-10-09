# Combinations III
------------------
@ [Description](https://leetcode.com/problems/combination-sum-iii/)  
@ Tags: Array, Backtracking   
@ Medium

------------------
## Solution - DFS
```java
class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> res = new ArrayList<>();
        if (k == 0)
            return res;
        helper(k, n, 1, new ArrayList<Integer>(), res);
        return res;
    }
    
    private void helper(int k, int n, int start, ArrayList<Integer> tmp, List<List<Integer>> res) {
        if (tmp.size() == k && n == 0) {
            res.add(new ArrayList<Integer>(tmp));
            return;
        }
        for (int i = start; i <= 9; i++) {
            if (i > n)
                break;
            tmp.add(i);
            helper(k, n - i, i + 1, tmp, res);
            tmp.remove(tmp.size() - 1);
        }
    }
}
```
