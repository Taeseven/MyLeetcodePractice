# Course Schedule
------------------
@ [Description](https://leetcode.com/problems/course-schedule/)  
@ Tags: DFS, BFSm Graph, Topological Sort   
@ Medium

------------------
## Solution - BFS + Topological Sort
先计算每个课程的indegree值，然后将indegree=0的课程放入queue中，利用BFS遍历求解。  
时间复杂度为：$O(E)$  
空间复杂度为：$O(V)$
```java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        if (prerequisites == null) return true;
        
        int[] count = getCount(numCourses, prerequisites);
        Map<Integer, Set<Integer>> map = getGraph(numCourses, prerequisites);
        Queue<Integer> queue = new LinkedList<>();
        
//         Initial queue
        for (int i = 0; i < numCourses; i++) {
            if (count[i] == 0)
                queue.offer(i);
        }
//         Topological Sort
        int total = 0;
        while (!queue.isEmpty()) {
            int tmp = queue.poll();
            total++;
            for (int i : map.get(tmp)) {
                count[i]--;
                if (count[i] == 0)
                    queue.offer(i);
            }
        }
        return total == numCourses;
        
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
