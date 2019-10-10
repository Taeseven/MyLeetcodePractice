# Permutations II
------------------
@ [Description](https://leetcode.com/problems/permutations-ii/)  
@ Tags: Backtracking   
@ Medium

------------------
## Solution - DFS

```java
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        if (nums == null || nums.length == 0)
            return res;
        Arrays.sort(nums);
        helper(new ArrayList<Integer>(), nums, res, new boolean[nums.length]);
        return res;
    }
    
    private void helper(ArrayList<Integer> tmp, int[] nums, List<List<Integer>> res, boolean[] isUsed) {
        if (tmp.size() == nums.length) {
            res.add(new ArrayList<Integer>(tmp));
            return;
        }
        for (int i = 0; i < nums.length; i++) {
            // 判断前一个相同的数字是否已经被用过了，只有前一个被用过的情况才会考虑下一个。
            if (i > 0 && nums[i-1] == nums[i] && !isUsed[i-1]) 
                continue;
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
