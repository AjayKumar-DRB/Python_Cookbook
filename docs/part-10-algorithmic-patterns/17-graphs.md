# Graphs

## Introduction

A Graph is a collection of nodes (vertices) connected by edges. Trees and Linked Lists are actually just specialized, restricted types of graphs.

In interviews, graphs are used to represent networks, relationships, maps, and state machines.

---

## How to Recognize It

Use Graph algorithms when:
- The problem involves a grid/matrix where you can move up, down, left, right (e.g., Number of Islands).
- The problem explicitly describes cities connected by roads, users connected by friendships, or tasks with prerequisites.

---

## Graph Representation

In Python, the most efficient and common way to represent a graph is using an **Adjacency List**, implemented with a `collections.defaultdict(list)`.

```python
from collections import defaultdict

# Representing edges: [start, end]
edges = [[0, 1], [0, 2], [1, 2], [2, 3]]

graph = defaultdict(list)

for u, v in edges:
    graph[u].append(v)
    # If the graph is undirected, you must add the reverse edge!
    graph[v].append(u) 

print(graph)
# {0: [1, 2], 1: [0, 2], 2: [0, 1, 3], 3: [2]}
```

---

## Traversing a Graph

Graph traversal is identical to Tree traversal, with one massive difference: **Graphs can have cycles.** 

If you do not track which nodes you have already visited, your traversal will loop infinitely. You must use a `visited` set.

### 1. Graph DFS (Recursion)
Used for finding connected components, detecting cycles, or exploring all paths.

```python
def dfs(node, graph, visited):
    if node in visited:
        return
        
    visited.add(node)
    print(node)
    
    for neighbor in graph[node]:
        dfs(neighbor, graph, visited)
```

### 2. Graph BFS (Queue)
Used for finding the **shortest path** in an unweighted graph.

```python
from collections import deque

def bfs_shortest_path(start, target, graph):
    # Queue stores tuples of (node, distance)
    queue = deque([(start, 0)])
    visited = set([start])
    
    while queue:
        node, dist = queue.popleft()
        
        if node == target:
            return dist
            
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append((neighbor, dist + 1))
                
    return -1 # Path not found
```

---

## Matrix as a Graph

Many FAANG questions present a 2D matrix (like a maze) instead of explicit edges. The nodes are the cells `(row, col)`, and the edges are the adjacent cells (Up, Down, Left, Right).

```python
def get_neighbors(matrix, r, c):
    ROWS = len(matrix)
    COLS = len(matrix[0])
    neighbors = []
    
    # Up, Down, Left, Right directions
    directions = [(-1, 0), (1, 0), (0, -1), (0, 1)]
    
    for dr, dc in directions:
        nr, nc = r + dr, c + dc
        # Check boundaries
        if 0 <= nr < ROWS and 0 <= nc < COLS:
            neighbors.append((nr, nc))
            
    return neighbors
```

---

## Time and Space Complexity

Let $V$ be the number of Vertices (nodes) and $E$ be the number of Edges.
- **Time Complexity**: $O(V + E)$ for both DFS and BFS, as you visit every node and explore every edge once.
- **Space Complexity**: $O(V + E)$ to store the adjacency list, plus $O(V)$ for the `visited` set and recursion stack/queue.

---

## Summary
- Represent graphs using `defaultdict(list)`.
- **Always use a `visited` set** to prevent infinite loops.
- Use **DFS** to explore all paths or find connected components.
- Use **BFS** to find the shortest path in unweighted graphs.
