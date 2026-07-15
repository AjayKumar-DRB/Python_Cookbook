# Hard Capstone: Course Schedule II

> **Time Limit:** 45 Minutes
> **Patterns:** Directed Graphs, Topological Sort (Kahn's or DFS)

---

## The Prompt

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [a, b]` indicates that you **must** take course `b` first if you want to take course `a`.

Return the ordering of courses you should take to finish all courses. If there are many valid answers, return any of them. If it is impossible to finish all courses, return an empty array.

**Example 1:**
```
Input: numCourses = 4, prerequisites = [[1,0],[2,0],[3,1],[3,2]]
Output: [0,2,1,3]
Explanation: There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0.
So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3].
```

**Constraints:**
- `1 <= numCourses <= 2000`
- `0 <= prerequisites.length <= numCourses * (numCourses - 1)`
- `prerequisites[i].length == 2`
- All the pairs `[a, b]` are distinct.

---

*Stop scrolling. Set a 45-minute timer and write your solution before checking the answer below.*

---

## The Solution Walkthrough

### 1. Understand & Match
We have dependencies (A must come before B). We need to output a valid linear ordering. This is the literal definition of **Topological Sort** on a Directed Graph.
If it is impossible to finish the courses, it means there is a circular dependency (a Cycle).

### 2. Plan (Kahn's Algorithm - BFS)
There are two ways to do Topological Sort: DFS with 3 states, or Kahn's Algorithm (BFS with In-Degrees). Kahn's is often much easier to explain in an interview.

1. Build an Adjacency List `adj = {course: [dependents]}`.
2. Build an `in_degree` array, where `in_degree[c]` is the number of prerequisites course `c` needs.
3. Find all courses with `in_degree == 0` (courses with no prerequisites) and put them in a Queue.
4. While the Queue is not empty:
   - Pop a course, add it to our `result` list.
   - For every dependent neighbor of that course, decrement their `in_degree` by 1.
   - If a neighbor's `in_degree` hits 0, push it to the Queue.
5. If the `result` list has the same length as `numCourses`, we successfully took all courses. Otherwise, there was a cycle, so return `[]`.

### 3. Implement

```python
import collections

class Solution:
    def findOrder(self, numCourses: int, prerequisites: list[list[int]]) -> list[int]:
        # 1. Initialize Adjacency List and In-Degree array
        adj = collections.defaultdict(list)
        in_degree = [0] * numCourses
        
        # 2. Build the Graph
        # pre[1] must be taken before pre[0]
        # So the directed edge is pre[1] -> pre[0]
        for course, pre in prerequisites:
            adj[pre].append(course)
            in_degree[course] += 1
            
        # 3. Find all courses with 0 prerequisites
        q = collections.deque()
        for i in range(numCourses):
            if in_degree[i] == 0:
                q.append(i)
                
        # 4. Process the Queue (Kahn's Algorithm)
        order = []
        while q:
            current = q.popleft()
            order.append(current)
            
            for neighbor in adj[current]:
                in_degree[neighbor] -= 1
                # If all prerequisites for neighbor are fulfilled
                if in_degree[neighbor] == 0:
                    q.append(neighbor)
                    
        # 5. Check if we processed all courses (detect cycles)
        if len(order) == numCourses:
            return order
        else:
            return []
```

### 4. Complexity Analysis
- **Time Complexity:** $O(V + E)$ where $V$ is `numCourses` and $E$ is the number of `prerequisites`. We build the graph in $O(E)$ time, scan the in-degrees in $O(V)$ time, and the BFS queue processes every node and edge exactly once.
- **Space Complexity:** $O(V + E)$. The Adjacency List takes $O(E)$ space, and the Queue / Output array take $O(V)$ space.
