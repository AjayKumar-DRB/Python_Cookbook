# `collections.deque`

## Introduction

The `deque` (pronounced "deck", standing for **d**ouble-**e**nded **que**ue) is a list-like container that provides $O(1)$ time complexity for append and pop operations from **both ends**.

If you need a Queue (FIFO) or a sliding window in Python, you must use a `deque`.

---

## Why Standard Lists Fail as Queues

As discussed in the Lists section, standard Python lists are implemented as dynamic arrays. 

While `list.append()` and `list.pop()` (at the end) are amortized $O(1)$, removing an element from the front using `list.pop(0)` is $O(N)$ because every remaining element must be shifted one position to the left.

If you process $N$ elements in a queue using a standard list, your algorithm degrades to $O(N^2)$. A `deque` avoids this.

---

## Using `deque`

You must import it from the `collections` module.

```python
from collections import deque

# Initialize an empty deque
q = deque()

# Initialize from an iterable
q = deque([1, 2, 3])
```

### The 4 Core $O(1)$ Operations

```python
q = deque([2, 3])

# 1. Append to the right (end)
q.append(4)    # deque([2, 3, 4])

# 2. Append to the left (front)
q.appendleft(1) # deque([1, 2, 3, 4])

# 3. Pop from the right (end)
last = q.pop()      # returns 4, deque is [1, 2, 3]

# 4. Pop from the left (front)
first = q.popleft() # returns 1, deque is [2, 3]
```

---

## Interview Application: BFS (Breadth-First Search)

The most common use of a `deque` is implementing BFS on a graph or a tree.

```python
from collections import deque

def bfs(root):
    if not root:
        return
        
    queue = deque([root])
    
    while queue:
        # O(1) removal from the front
        node = queue.popleft() 
        
        print(node.val)
        
        if node.left:
            queue.append(node.left)
        if node.right:
            queue.append(node.right)
```

---

## Deque Implementation Limitations

While `deque` is amazing at the ends, it is **terrible in the middle**.

A `deque` is implemented as a doubly-linked list of fixed-length memory blocks.
- **Fast Ends**: Adding or removing from ends is $O(1)$.
- **Slow Indexing**: Accessing an element in the middle `q[k]` takes $O(K)$ time. If you need fast random access, use a standard list.

---

## Summary
- Use `from collections import deque` to implement Queues.
- `append()` and `pop()` operate on the right end ($O(1)$).
- `appendleft()` and `popleft()` operate on the left end ($O(1)$).
- **Never** use `list.pop(0)` in an interview. Use `deque.popleft()`.
- Avoid using `deque` if you need to access elements by index in the middle.
