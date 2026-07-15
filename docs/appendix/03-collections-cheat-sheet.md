# Collections Cheat Sheet

The `collections` module provides specialized container datatypes.

```python
import collections
```

## 1. deque (Double-Ended Queue)
Thread-safe, $O(1)$ appends and pops from both ends. Essential for BFS.

```python
q = collections.deque([1, 2, 3])

q.append(4)      # [1, 2, 3, 4]
q.appendleft(0)  # [0, 1, 2, 3, 4]

right = q.pop()      # 4
left = q.popleft()   # 0
```

## 2. Counter
A dictionary subclass for counting hashable objects.

```python
counts = collections.Counter("hello")
# Counter({'l': 2, 'h': 1, 'e': 1, 'o': 1})

# Get most common elements
print(counts.most_common(1)) # [('l', 2)]

# Math with Counters
c1 = collections.Counter(a=3, b=1)
c2 = collections.Counter(a=1, b=2)
print(c1 + c2) # Counter({'a': 4, 'b': 3})
print(c1 - c2) # Counter({'a': 2}) # Negatives are removed
```

## 3. defaultdict
A dictionary that calls a factory function to supply missing values.

```python
# Default to integer (0)
d_int = collections.defaultdict(int)
d_int["apples"] += 1

# Default to list ([])
d_list = collections.defaultdict(list)
d_list["fruits"].append("apple")

# Graph Adjacency List
graph = collections.defaultdict(list)
for u, v in edges:
    graph[u].append(v)
```
