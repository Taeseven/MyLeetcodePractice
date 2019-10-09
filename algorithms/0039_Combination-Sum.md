# Combinations
------------------
@ [Description](https://leetcode.com/problems/combination-sum/)  
@ Tags: Array, Backtracking   
@ Medium

------------------
## Solution - DFS
注意可以重复选择同一数字，若剩余数字均大于target要跳出循环。
```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> res = new ArrayList<>();
        if (candidates == null || candidates.length == 0)
            return res;
        Arrays.sort(candidates);
        helper(candidates, 0, target, new ArrayList<Integer>(), res);
        return res;
    }
    
    private void helper(int[] nums, int start, int target, ArrayList<Integer> tmp, List<List<Integer>> res) {
        if (target == 0) {
            res.add(new ArrayList<Integer>(tmp));
            return;
        }
        for (int i = start; i < nums.length; i++) {
            if (nums[i] > target)
                break;
            tmp.add(nums[i]);
            helper(nums, i, target - nums[i], tmp, res);
            tmp.remove(tmp.size() - 1);
        }
    }
}
```
