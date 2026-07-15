# Collections Interview Recipes

## Introduction

The `collections` module provides specialized tools that act as "cheat codes" for common interview problems. Memorize these recipes to instantly solve BFS, LRU Cache, and Frequency questions.

---

## Recipe 1: Breadth-First Search (BFS) with `deque`

Whenever you are traversing a tree or graph level-by-level, you must use a `deque` for $O(1)$ queue operations.

```python
from collections import deque

def bfs(start_node):
    queue = deque([start_node])
    visited = set([start_node])
    
    while queue:
        # Pop from the front
        node = queue.popleft()
        
        for neighbor in node.neighbors:
            if neighbor not in visited:
                visited.add(neighbor)
                # Append to the back
                queue.append(neighbor)
```

---

## Recipe 2: Top K Frequent Elements with `Counter`

When asked to find the most frequent, least frequent, or missing elements, `Counter` handles the logic for you.

```python
from collections import Counter

def top_k_frequent(nums, k):
    counts = Counter(nums)
    # Returns [(element, count), ...]
    return [element for element, count in counts.most_common(k)]
```

---

## Recipe 3: Building a Graph Adjacency List

When parsing a list of edges into a graph representation, use `defaultdict(list)` to avoid checking if keys exist.

```python
from collections import defaultdict

def build_graph(edges):
    graph = defaultdict(list)
    
    for u, v in edges:
        graph[u].append(v)
        graph[v].append(u) # If undirected
        
    return graph
```

---

## Recipe 4: LRU Cache Implementation

When asked to design a Least Recently Used cache, use `OrderedDict`.

```python
from collections import OrderedDict

class LRUCache:
    def __init__(self, capacity: int):
        self.cache = OrderedDict()
        self.capacity = capacity

    def get(self, key: int) -> int:
        if key not in self.cache:
            return -1
        self.cache.move_to_end(key) # Mark recently used
        return self.cache[key]

    def put(self, key: int, value: int) -> None:
        self.cache[key] = value
        self.cache.move_to_end(key)
        if len(self.cache) > self.capacity:
            self.cache.popitem(last=False) # Evict oldest
```

---

## Recipe 5: Readable BFS States

If your queue contains complex states (coordinates, distance, keys collected), use a `namedtuple`.

```python
from collections import deque, namedtuple

def shortest_path(grid):
    State = namedtuple('State', ['r', 'c', 'dist'])
    queue = deque([State(0, 0, 0)])
    
    while queue:
        curr = queue.popleft()
        print(f"Row: {curr.r}, Col: {curr.c}, Distance: {curr.dist}")
```

---

## Summary
- **Queue**: Use `deque` + `popleft()`.
- **Frequencies**: Use `Counter` + `most_common(k)`.
- **Graphs**: Use `defaultdict(list)`.
- **LRU Cache**: Use `OrderedDict` + `move_to_end(key)`.
- **Readability**: Use `namedtuple` for complex queue or heap states.
