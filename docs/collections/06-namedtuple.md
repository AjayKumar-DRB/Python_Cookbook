# `collections.namedtuple`

## Introduction

A `namedtuple` assigns meaning to each position in a tuple, allowing for more readable and self-documenting code. They can be used wherever regular tuples are used, but they add the ability to access fields by name instead of index.

While rarely strictly *required* to solve an algorithmic problem, using `namedtuple` makes complex data structures (like priority queue nodes or graph edges) much easier to read.

---

## Creating a NamedTuple

You create a `namedtuple` by passing a class name and a list of field names.

```python
from collections import namedtuple

# Create a Point class with x and y fields
Point = namedtuple('Point', ['x', 'y'])
```

### Instantiating

You can instantiate it using positional or keyword arguments.

```python
p1 = Point(10, 20)
p2 = Point(x=30, y=40)
```

---

## Accessing Fields

You can access fields exactly like a regular tuple (using indices) or by name (using dot notation).

```python
p = Point(10, 20)

# Access by index (like a regular tuple)
print(p[0]) # 10

# Access by name (much more readable)
print(p.x)  # 10
print(p.y)  # 20
```

---

## When to use in Interviews

### 1. BFS/DFS States
When searching through a grid or a maze, your queue often needs to store the current row, column, and distance (or cost). 

Using a standard tuple `(r, c, dist)` works, but accessing `node[2]` is hard to read.

```python
# Unreadable
queue.append((0, 0, 1))
current = queue.pop(0)
cost = current[2]

# Readable
State = namedtuple('State', ['r', 'c', 'dist'])
queue.append(State(0, 0, 1))
current = queue.pop(0)
cost = current.dist
```

### 2. A* or Dijkstra's Algorithm
When pushing items onto a priority queue (`heapq`), the heap sorts by the first element of the tuple. A `namedtuple` makes it clear what the sorting key is.

```python
Node = namedtuple('Node', ['cost', 'id', 'path'])

# The heap will automatically sort by 'cost' (the first field)
heapq.heappush(pq, Node(cost=10, id="A", path=["Start", "A"]))
```

---

## Immutability

Like regular tuples, `namedtuple` instances are **immutable**. You cannot change the value of an attribute after creation.

```python
p = Point(10, 20)
# p.x = 100 # AttributeError: can't set attribute
```
Because they are immutable, they are hashable and can be used as dictionary keys or added to sets.

---

## Time and Space Complexity

- **Time Complexity**: $O(1)$ creation and access, identical to a standard tuple.
- **Space Complexity**: Memory overhead is equivalent to a standard tuple. It does not carry the memory overhead of a full custom class dictionary.

---

## Summary
- Use `namedtuple` to assign names to tuple indices.
- Makes BFS queue states and Dijkstra heap nodes highly readable.
- Accessed via dot notation (`node.cost`).
- Fully immutable and hashable, just like regular tuples.
