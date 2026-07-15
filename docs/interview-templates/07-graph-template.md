# Graph Templates

## Graph Construction Template

The overwhelming majority of Graph problems give you a list of edges. You must build an Adjacency List before traversing.

```python
from collections import defaultdict

def build_graph(num_nodes, edges):
    graph = defaultdict(list)
    
    for u, v in edges:
        graph[u].append(v)
        graph[v].append(u) # OMIT this line if the graph is DIRECTED
        
    return graph
```

## Graph Traversal Template (DFS with Cycle Detection)

```python
def has_path(graph, start, target):
    visited = set()
    
    def dfs(node):
        if node == target:
            return True
            
        if node in visited:
            return False
            
        visited.add(node)
        
        for neighbor in graph[node]:
            if dfs(neighbor):
                return True
                
        return False
        
    return dfs(start)
```

## Topological Sort Template (Kahn's Algorithm)

```python
from collections import defaultdict, deque

def topological_sort(num_nodes, edges):
    graph = defaultdict(list)
    in_degree = {i: 0 for i in range(num_nodes)}
    
    # Build Directed Graph and In-Degrees
    for prereq, course in edges:
        graph[prereq].append(course)
        in_degree[course] += 1
        
    # Start with nodes having 0 prerequisites
    queue = deque([k for k, v in in_degree.items() if v == 0])
    order = []
    
    while queue:
        node = queue.popleft()
        order.append(node)
        
        for neighbor in graph[node]:
            in_degree[neighbor] -= 1
            if in_degree[neighbor] == 0:
                queue.append(neighbor)
                
    # Return order if all nodes processed (no cycle), else empty
    return order if len(order) == num_nodes else []
```
