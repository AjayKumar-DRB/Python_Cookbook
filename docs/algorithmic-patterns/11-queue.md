# Queue

## Introduction

A Queue is a FIFO (First-In, First-Out) data structure. The first element added to the queue will be the first one removed.

Unlike Stacks, **you cannot use a standard Python `list` for a Queue** if you care about performance.

---

## The List Trap

If you use a list and call `list.pop(0)` to remove the first element, Python has to shift every remaining element one index to the left. 

This makes popping from the front an $O(N)$ operation. In an algorithm like Breadth-First Search (BFS) that processes $N$ nodes, using `pop(0)` degrades your time complexity from $O(N)$ to $O(N^2)$.

---

## The Pythonic Implementation: `collections.deque`

You must use a `deque` (double-ended queue) from the `collections` module. It provides $O(1)$ time complexity for appending and popping from both ends.

```python
from collections import deque

# Initialize
queue = deque()

# Enqueue (Push to the back) - O(1)
queue.append("A")
queue.append("B")
queue.append("C")

# Dequeue (Pop from the front) - O(1)
print(queue.popleft()) # "A"
print(queue.popleft()) # "B"
```

---

## How to Recognize It

Use a Queue when:
- You are implementing Breadth-First Search (BFS) on a graph or tree.
- You need to process items in the exact order they arrived (e.g., Task Scheduling).
- You are maintaining a Sliding Window of a specific time frame.

---

## Breadth-First Search (BFS) Template

This is the most common use of a queue in interviews.

```python
from collections import deque

def bfs(start_node):
    queue = deque([start_node])
    visited = set([start_node])
    
    while queue:
        # 1. Pop from the front
        node = queue.popleft()
        
        # 2. Process node
        print(node.val)
        
        # 3. Add neighbors to the back
        for neighbor in node.neighbors:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
```

---

## Time and Space Complexity

- **Time Complexity**: $O(1)$ for `append()` and `popleft()`.
- **Space Complexity**: $O(N)$ where $N$ is the maximum number of items in the queue.

---

## Summary
- **Never** use `list.pop(0)` for a queue in an interview.
- Always `import deque from collections`.
- Use `append()` to enqueue and `popleft()` to dequeue in $O(1)$ time.
- Queues are the backbone of Breadth-First Search (BFS).
