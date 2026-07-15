# `collections.OrderedDict`

## Introduction

An `OrderedDict` is a dictionary subclass that remembers the order in which its contents were added.

Since Python 3.7, the standard `dict` also maintains insertion order. However, `OrderedDict` is still heavily tested in interviews because of its specialized methods for rearranging elements, making it the secret weapon for Cache design questions.

---

## When to Use `OrderedDict`

In modern Python, you do not need `OrderedDict` just to iterate over keys in order. You only need it when you specifically need to manipulate the order of elements.

### The LRU Cache Problem
The "Design an LRU (Least Recently Used) Cache" problem is one of the most famous interview questions (e.g., LeetCode 146).

An LRU Cache needs:
1. $O(1)$ lookups (like a hash map).
2. $O(1)$ evictions of the oldest element (like a queue or linked list).

Under the hood, an `OrderedDict` is implemented using a hash map combined with a doubly-linked list, providing exactly these properties. 

If the interviewer allows you to use `OrderedDict`, you can implement an LRU cache in fewer than 15 lines of code.

---

## The `move_to_end()` Method

The killer feature of `OrderedDict` is `move_to_end(key, last=True)`. It moves an existing key to either the right end (most recently used) or the left end (least recently used) in $O(1)$ time.

```python
from collections import OrderedDict

# Create an OrderedDict
cache = OrderedDict()
cache["A"] = 1
cache["B"] = 2
cache["C"] = 3

# Move "A" to the end (Most Recently Used)
cache.move_to_end("A")
print(cache)
# OrderedDict([('B', 2), ('C', 3), ('A', 1)])

# Move "A" to the front (Least Recently Used)
cache.move_to_end("A", last=False)
print(cache)
# OrderedDict([('A', 1), ('B', 2), ('C', 3)])
```

---

## The `popitem()` Method

The `popitem(last=True)` method removes and returns a `(key, value)` pair.
- If `last=True` (default), it acts like a stack (LIFO), popping the most recently added item.
- If `last=False`, it acts like a queue (FIFO), popping the oldest item.

```python
cache = OrderedDict([('A', 1), ('B', 2), ('C', 3)])

# Evict the oldest item (LRU policy)
oldest = cache.popitem(last=False)
print(oldest) # ('A', 1)
```

---

## Implementing an LRU Cache

Here is the optimal implementation of an LRU cache using `OrderedDict`.

```python
from collections import OrderedDict

class LRUCache:
    def __init__(self, capacity: int):
        self.cache = OrderedDict()
        self.capacity = capacity

    def get(self, key: int) -> int:
        if key not in self.cache:
            return -1
            
        # Move to end to mark as recently used
        self.cache.move_to_end(key)
        return self.cache[key]

    def put(self, key: int, value: int) -> None:
        if key in self.cache:
            # Update and mark as recently used
            self.cache[key] = value
            self.cache.move_to_end(key)
        else:
            # Add new key
            self.cache[key] = value
            
            # Evict if over capacity
            if len(self.cache) > self.capacity:
                self.cache.popitem(last=False)
```

*(Note: While some strict interviewers may demand you implement the Doubly Linked List yourself, writing this first proves you know standard library tools).*

---

## Summary
- Use `OrderedDict` specifically for LRU Cache implementations.
- Use `move_to_end(key)` to mark an item as recently used in $O(1)$ time.
- Use `popitem(last=False)` to evict the oldest item in $O(1)$ time.
