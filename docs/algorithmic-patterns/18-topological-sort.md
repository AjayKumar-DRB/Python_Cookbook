# Topological Sort

## Introduction

Topological Sort is a graph algorithm used exclusively on **Directed Acyclic Graphs (DAGs)**.

It provides a linear ordering of vertices such that for every directed edge $U \rightarrow V$, vertex $U$ comes before vertex $V$ in the ordering.

---

## How to Recognize It

Use Topological Sort when:
- The problem involves **prerequisites** or dependencies (e.g., Course Schedule, Build Systems, Package Managers).
- You need to find a valid execution order for a set of tasks.
- The problem asks if a cycle exists in a directed graph.

---

## Kahn's Algorithm (BFS Approach)

The most intuitive way to implement Topological Sort is Kahn's Algorithm, which uses the concept of **In-Degree** (the number of edges pointing *into* a node).

1. Calculate the in-degree of every node.
2. Place all nodes with an in-degree of 0 (no prerequisites) into a Queue.
3. While the queue is not empty, pop a node and add it to the final order.
4. For each neighbor of the popped node, reduce its in-degree by 1 (simulating the completion of a prerequisite).
5. If a neighbor's in-degree drops to 0, push it to the queue.

### Example: Course Schedule
```python
from collections import defaultdict, deque

def find_order(num_courses, prerequisites):
    # 1. Initialize graph and in-degrees
    graph = defaultdict(list)
    in_degree = {i: 0 for i in range(num_courses)}
    
    # 2. Build graph (prereq -> course)
    for course, prereq in prerequisites:
        graph[prereq].append(course)
        in_degree[course] += 1
        
    # 3. Find all courses with 0 prerequisites
    queue = deque([k for k, v in in_degree.items() if v == 0])
    
    order = []
    
    # 4. Process the queue
    while queue:
        node = queue.popleft()
        order.append(node)
        
        # Complete this course, unlocking neighbors
        for neighbor in graph[node]:
            in_degree[neighbor] -= 1
            if in_degree[neighbor] == 0:
                queue.append(neighbor)
                
    # 5. Cycle Detection
    # If the order doesn't contain all courses, a cycle exists
    if len(order) == num_courses:
        return order
    else:
        return []
```

---

## Why Kahn's over DFS?

You can also perform Topological Sort using DFS (by adding nodes to an array post-order and reversing it). 

However, Kahn's algorithm (BFS) is generally preferred in interviews because:
1. It naturally handles **cycle detection** (if the final order length is less than the number of nodes, a cycle exists).
2. It is iterative, avoiding recursion limits.
3. It easily supports advanced variations, like returning the *lexicographically smallest* order (just swap the `deque` for a `heapq`!).

---

## Time and Space Complexity

- **Time Complexity**: $O(V + E)$ where $V$ is vertices (courses) and $E$ is edges (prerequisites). We process each node and each edge exactly once.
- **Space Complexity**: $O(V + E)$ to store the adjacency list graph and the in-degree tracking map.

---

## Summary
- Use Topological Sort for **prerequisite/dependency** problems.
- Track the **In-Degree** of every node.
- Push nodes with `in_degree == 0` to a Queue.
- Pop nodes, decrement neighbor in-degrees, and push neighbors when they hit 0.
- If the final output size doesn't match total nodes, a cycle prevented completion.
