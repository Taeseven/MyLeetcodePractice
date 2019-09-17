# Find the Duplicate Number
@ [Description](https://leetcode.com/problems/find-the-duplicate-number/)  
@ Tags: Array, Linked List      
@ Medium

------------------
## Solution 1 - Sorting
先对array进行排序，然后遍历看前后项是否相等。  
时间复杂度：$O(NlogN)$  
空间复杂度：$O(1)$  

## Solution 2 - Set
遍历array将元素存在set中，若set中已存在该参数则返回。
时间复杂度：$O(N)$  
空间复杂度：$O(N)$

## Solution 3 - Floyd's Tortoise and Hare (Cycle Detection)
可以将其假象成Linked List，若存在重复的数字则一定存在环。  
每次value的就是下一次的index。利用两个快慢指针，慢指针每次移动一个步长，快指针每次移动两个步长。两个指针最终一定会在环中某一位置相遇。  
此时，将快指针重置到表头，每次移动一个步长。慢指针继续按一个步长移动。那么这两个指针第一次相遇的点一定是环的入口，即表中唯一个重复的数字。  
时间复杂度：$O(N)$  
空间复杂度：$O(1)$  
相关题目：[Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/)  
[相关解答](https://blog.csdn.net/willduan1/article/details/50938210)
```java
class Solution {
    public int findDuplicate(int[] nums) {
        int slow = nums[0];
        int fast = nums[0];
        
        do {
            slow = nums[slow];
            fast = nums[nums[fast]];
        } while (slow != fast);
        
        int ptr1 = nums[0];
        int ptr2 = slow;
        while (ptr1 != ptr2) {
            ptr1 = nums[ptr1];
            ptr2 = nums[ptr2];
        }
        return ptr1;
    }
}
```
