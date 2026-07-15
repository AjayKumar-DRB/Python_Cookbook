# Heapq Cheat Sheet

Python's `heapq` module provides an implementation of the heap queue algorithm, also known as the priority queue algorithm.
**Python only natively supports Min-Heaps.**

```python
import heapq
```

## 1. Creating a Heap
Transform a list into a heap in-place.
- **Time Complexity:** $O(N)$

```python
nums = [5, 7, 9, 1, 3]
heapq.heapify(nums)
# nums is now [1, 3, 9, 7, 5] 
# The smallest element is always at index 0
```

## 2. Pushing and Popping
- **Time Complexity:** $O(\log N)$ for both operations.

```python
# Push
heapq.heappush(nums, 2)

# Pop the smallest item
smallest = heapq.heappop(nums)
```

## 3. Push-Pop Combinations
These are slightly more efficient than calling push then pop separately.

```python
# Push item on the heap, then pop and return the smallest item
heapq.heappushpop(nums, 10)

# Pop and return the smallest item, then push the new item
heapq.heapreplace(nums, 10)
```

## 4. N-Largest and N-Smallest
Find the top K elements. This is equivalent to `sorted(iterable)[:n]`, but faster for small `n`.
- **Time Complexity:** $O(N \log K)$

```python
nums = [5, 7, 9, 1, 3]

# Get the 2 largest elements
largest = heapq.nlargest(2, nums) # [9, 7]

# Get the 3 smallest elements
smallest = heapq.nsmallest(3, nums) # [1, 3, 5]
```

## 5. Simulating a Max-Heap
Since Python only has a Min-Heap, multiply your values by `-1` before pushing, and `-1` again after popping.

```python
max_heap = []
heapq.heappush(max_heap, -10)
heapq.heappush(max_heap, -5)

largest = -heapq.heappop(max_heap) # 10
```
