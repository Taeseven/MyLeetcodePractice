# Permutations
------------------
@ [Description](https://leetcode.com/problems/permutations/)  
@ Tags: Backtracking   
@ Medium

------------------
## Solution - DFS
时间及空间负责度均为: $O(N!)$
```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        if (nums == null || nums.length == 0)
            return res;
        helper(new ArrayList<Integer>(), nums, res, new boolean[nums.length]);
        return res;
    }
    
    private void helper(ArrayList<Integer> tmp, int[] nums, List<List<Integer>> res, boolean[] isUsed) {
        if (tmp.size() == nums.length) {
            res.add(new ArrayList<Integer>(tmp));
            return;
        }
        for (int i = 0; i < nums.length; i++) {
            if (!isUsed[i]) {
                tmp.add(nums[i]);
                isUsed[i] = true;
                helper(tmp, nums, res, isUsed);
                tmp.remove(tmp.size() - 1);
                isUsed[i] = false;
            }
        }
    }
}
```
