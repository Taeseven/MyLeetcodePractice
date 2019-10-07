# Course Schedule II
------------------
@ [Description](https://leetcode.com/problems/course-schedule-ii/)  
@ Tags: DFS, BFSm Graph, Topological Sort   
@ Medium

------------------
## Solution - BFS + Topological Sort
与Leetcode 207一致。  
```java
class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        int[] res = new int[numCourses];
        if (prerequisites == null) return res;
        
        int[] count = getCount(numCourses, prerequisites);
        Map<Integer, Set<Integer>> map = getGraph(numCourses, prerequisites);
        Queue<Integer> queue = new LinkedList<>();
        
//         Initial queue
        int index = 0;
        for (int i = 0; i < numCourses; i++) {
            if (count[i] == 0) {
                queue.offer(i);
                res[index++] = i;
            }
        }
//         Topological Sort
        int total = 0;
        while (!queue.isEmpty()) {
            int tmp = queue.poll();
            total++;
            for (int i : map.get(tmp)) {
                count[i]--;
                if (count[i] == 0) {
                    queue.offer(i);
                    res[index++] = i;
                }
            }
        }
        return (total == numCourses) ? res : new int[0];
        
    }
    
    private int[] getCount(int n, int[][] pre) {
        int[] count = new int[n];
        Arrays.fill(count, 0);
        for (int[] course : pre) {
            count[course[0]]++;
        }
        return count;
    }
    
    private Map<Integer, Set<Integer>> getGraph(int n, int[][] pre) {
        Map<Integer, Set<Integer>> course = new HashMap<>();
        for (int i = 0; i < n; i++) {
            course.put(i, new HashSet<Integer>());
        }
        for (int[] edges : pre) {
            course.get(edges[1]).add(edges[0]);
        }
        return course;
    }
}
```
