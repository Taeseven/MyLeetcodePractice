# Subsets
------------------
@ [Description](https://leetcode.com/problems/subsets/)  
@ Tags: Array, Backtracking   
@ Medium

------------------
## Solution - DFS
```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        if (nums == null || nums.length == 0)
            return res;
        helper(nums, 0, new ArrayList<Integer>(), res);
        return res;
    }
    
    private void helper(int[] nums, int start, ArrayList<Integer> tmp, List<List<Integer>> res) { 
        res.add(new ArrayList<Integer>(tmp));
        for (int i = start; i < nums.length; i++) {
            // [1] -> [1,2]
            tmp.add(nums[i]);
            // search [1,2] as begining
            helper(nums, i+1, tmp, res);
            // [1,2] -> [1]
            tmp.remove(tmp.size() - 1);
        }
    }
}
```
