# Combinations
------------------
@ [Description](https://leetcode.com/problems/combinations/)  
@ Tags: Backtracking   
@ Medium

------------------
## Solution - DFS
```java
class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> res = new ArrayList<>();
        if (k == 0)
            return res;
        helper(n, 1, k, new ArrayList<Integer>(), res);
        return res;
    }
    
    private void helper(int n, int start, int k, ArrayList<Integer> tmp, List<List<Integer>> res) {
        if (tmp.size() == k) {
            res.add(new ArrayList<Integer>(tmp));
            return;
        }
        for (int i = start; i <= n; i++) {
            tmp.add(i);
            helper(n, i+1, k, tmp, res);
            tmp.remove(tmp.size() - 1);
        }
    }
}
```
