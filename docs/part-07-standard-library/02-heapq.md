# `heapq` (Priority Queues)

## Introduction

A Heap (specifically a Min-Heap) is a binary tree structure that always keeps the smallest element at the top. It is the underlying data structure for a **Priority Queue**.

Python implements heaps using the `heapq` module. Rather than providing a distinct `Heap` class, `heapq` provides functions that manipulate a standard Python `list`.

---

## Creating a Min-Heap

By default, `heapq` creates a **Min-Heap**.

```python
import heapq

# Start with an empty list
pq = []

# Push elements (O(log N))
heapq.heappush(pq, 5)
heapq.heappush(pq, 1)
heapq.heappush(pq, 3)

# The smallest element is always at index 0
print(pq[0]) # 1
```

### Heapifying an Existing List

If you already have a list of numbers, you can transform it into a valid heap in $O(N)$ time using `heapify()`. This is faster than pushing elements one by one (which takes $O(N \log N)$).

```python
nums = [5, 1, 9, 3, 7]
heapq.heapify(nums)

print(nums[0]) # 1
```

---

## Popping Elements

Use `heappop()` to remove and return the smallest element. The heap automatically rebalances itself in $O(\log N)$ time.

```python
smallest = heapq.heappop(nums)
print(smallest) # 1
print(nums[0])  # 3 (the new smallest)
```

---

## Creating a Max-Heap

Python does **not** have a built-in Max-Heap. 

To simulate a Max-Heap, you must **invert the values** (multiply by `-1`) before pushing them onto the heap, and invert them again when popping.

```python
max_heap = []

# Push negative values
heapq.heappush(max_heap, -5)
heapq.heappush(max_heap, -1)
heapq.heappush(max_heap, -10)

# Pop and invert back
largest = -heapq.heappop(max_heap)
print(largest) # 10
```

---

## Pushing Custom Objects (Tuples)

If you need to store complex objects in a heap (like nodes in Dijkstra's algorithm), use tuples. `heapq` will sort by the first element of the tuple. If there is a tie, it compares the second element.

```python
pq = []

# Tuple format: (priority, data)
heapq.heappush(pq, (2, "Task B"))
heapq.heappush(pq, (1, "Task A"))
heapq.heappush(pq, (3, "Task C"))

# Pops the tuple with the lowest priority number
priority, task = heapq.heappop(pq)
print(task) # "Task A"
```

*(Note: If the first elements tie, and the second elements are uncomparable custom objects, Python will throw a `TypeError`. To fix this, use a `namedtuple` or add an `__lt__` magic method to your class).*

---

## `nlargest` and `nsmallest`

If a problem asks for the "Top K" elements, `heapq` provides two highly optimized functions. They are cleaner and often faster than sorting the entire list.

```python
nums = [1, 8, 2, 23, 7, -4, 18, 23, 42, 37, 2]

print(heapq.nlargest(3, nums))  # [42, 37, 23]
print(heapq.nsmallest(3, nums)) # [-4, 1, 2]
```
- **Time Complexity**: $O(N \log K)$

---

## Time and Space Complexity

- **`heapify(list)`**: $O(N)$ time, $O(1)$ extra space.
- **`heappush(heap, item)`**: $O(\log N)$ time.
- **`heappop(heap)`**: $O(\log N)$ time.
- **`heap[0]` (peek)**: $O(1)$ time.

---

## Summary
- `heapq` turns standard lists into Min-Heaps.
- Use `heapq.heapify(nums)` for $O(N)$ initialization.
- Use `-value` to simulate a Max-Heap.
- Use tuples `(priority, value)` to sort custom data.
- Use `nlargest(k, nums)` for Top K problems.
