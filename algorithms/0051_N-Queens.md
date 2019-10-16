# N-Queens
------------------
@ [Description](https://leetcode.com/problems/n-queens/)  
@ Tags: Backtracking   
@ Hard

------------------
## Solution - DFS
利用常见的DFS操作即可，注意需要对位置是否可行进行判断。  
由于输出格式较为复杂，可以考虑将结果简便的储存，当需要输出时再转换成所需要的格式。  
根据国际象棋的规则，每个queen的位置会决定其所在row，column以及两条对角线上不能有其他的queen。  
时间复杂度：$O(N!)$  
空间复杂度：$O(N)$  
```java
class Solution {
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> res = new ArrayList<>();
        helper(n, res, new ArrayList<Integer>(), new boolean[n]);
        return res;
    }
    
    private void helper(int n, List<List<String>> res, ArrayList<Integer> tmp, boolean[] isUsed) {
        if (tmp.size() == n) {
            outputHelper(n, res, tmp);
            return;
        }
        for (int i = 0; i < n; i++) {
            if (!isUsed[i]) {
                if (isValid(i, tmp)) {
                    tmp.add(i);
                    isUsed[i] = true;
                    helper(n, res, tmp, isUsed);
                    tmp.remove(tmp.size() - 1);
                    isUsed[i] = false;
                }
            }
        }
    }
    
    private boolean isValid(int i, ArrayList<Integer> tmp) {
        if (tmp.size() == 0)
            return true;
        for (int j = 0; j < tmp.size(); j++) {
            if (Math.abs(tmp.size() - j) == Math.abs(tmp.get(j) - i))
                return false;
        }
        return true;
    }
    
    private void outputHelper(int n, List<List<String>> res, ArrayList<Integer> tmp) {
        List<String> solution = new ArrayList<String>();
        for (int i = 0; i < n; i++) {
            int col = tmp.get(i);
            StringBuilder sb = new StringBuilder();
            for (int j = 0; j < n; j++)
                sb.append(col == j ? "Q" : ".");
            solution.add(sb.toString());
        }
        res.add(solution);
    }
}
```
