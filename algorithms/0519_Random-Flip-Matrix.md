# Random Flip Matrix
------------------
@ [Description](https://leetcode.com/problems/random-flip-matrix/)  
@ Tags: Random     
@ Medium

------------------
## Solution
```java
class Solution {
    int row, col, total;
    Set<Integer> set = new HashSet<>();
    Random rand = new Random();

    public Solution(int n_rows, int n_cols) {
        row = n_rows;
        col = n_cols;
        total = row * col;
    }
    
    public int[] flip() {
        int x;
        do {
            x = rand.nextInt(total);
        } while (set.contains(x));
        set.add(x);
        return new int[]{x / col, x % col};
    }
    
    public void reset() {
        set.clear();
    }
}
```
