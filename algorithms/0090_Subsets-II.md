# Subsets II
------------------
@ [Description](https://leetcode.com/problems/subsets-ii/)  
@ Tags: Array, Backtracking   
@ Medium

------------------
## Solution - DFS
与Leetcode 0078类似，因为存在duplicates所以要判断重复的情况，因而需要提前将nums进行排序。  
当传入helper function后，添加判断条件以防止会添加后续相同的数字进入我们的最终结果中，即若有与start位置一样的数字时跳过。
```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        if (nums == null || nums.length == 0)
            return res;
        Arrays.sort(nums);
        helper(nums, 0, new ArrayList<Integer>(), res);
        return res;
    }
    
    private void helper(int[] nums, int start, ArrayList<Integer> tmp, List<List<Integer>> res) { 
        res.add(new ArrayList<Integer>(tmp));
        for (int i = start; i < nums.length; i++) {
            // [1] -> [1,2]
            if (i != start && nums[i] == nums[i - 1])
                continue;
            tmp.add(nums[i]);
            // search [1,2] as begining
            helper(nums, i+1, tmp, res);
            // [1,2] -> [1]
            tmp.remove(tmp.size() - 1);
        }
    }
}
```
