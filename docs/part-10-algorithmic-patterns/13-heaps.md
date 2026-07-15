# Heaps (Priority Queues)

## Introduction

A Heap is a specialized tree-based data structure that satisfies the heap property: the parent node is always smaller (Min-Heap) or larger (Max-Heap) than its children.

This guarantees that the **root node is always the minimum or maximum element**.

---

## How to Recognize It

Use a Heap when:
- The problem asks for the **Top K**, **Kth Largest**, or **Kth Smallest** elements.
- You need to repeatedly extract the minimum/maximum element from a dynamic dataset.
- You are merging $K$ sorted arrays.
- You are implementing Dijkstra's algorithm for shortest paths in weighted graphs.

---

## The Pythonic Implementation: `heapq`

In Python, a heap is simply a standard `list` that is manipulated using the `heapq` module.

**Python only provides a Min-Heap natively.** The smallest element is always at index `0`.

```python
import heapq

nums = [5, 1, 9, 3]

# 1. Transform a list into a Min-Heap in-place (O(N))
heapq.heapify(nums)
print(nums[0]) # 1 (The minimum element)

# 2. Push an element (O(log N))
heapq.heappush(nums, 2)

# 3. Pop the smallest element (O(log N))
smallest = heapq.heappop(nums)
print(smallest) # 1
```

---

## Pattern 1: The Top K Elements

To find the Top $K$ largest elements, maintain a Min-Heap of size exactly $K$.

As you iterate through the data, push elements onto the heap. If the heap grows larger than $K$, pop the smallest element. At the end, the heap will contain exactly the $K$ largest elements.

```python
import heapq

def find_k_largest(nums, k):
    min_heap = []
    
    for num in nums:
        heapq.heappush(min_heap, num)
        # If heap is too large, drop the smallest element
        if len(min_heap) > k:
            heapq.heappop(min_heap)
            
    # The heap now contains the K largest elements
    return min_heap
```
*Time Complexity*: $O(N \log K)$. Space Complexity: $O(K)$. 
This is significantly faster than sorting the entire array ($O(N \log N)$) when $K$ is small.

---

## Pattern 2: Max-Heaps in Python

Because `heapq` only provides a Min-Heap, if you need a Max-Heap, you must **negate all the numbers** before pushing them, and negate them again when popping.

```python
import heapq

def max_heap_example(nums):
    max_heap = []
    
    for num in nums:
        # Push negative value
        heapq.heappush(max_heap, -num)
        
    # Pop and negate to get original value
    largest = -heapq.heappop(max_heap)
    return largest
```
*(Note: If pushing tuples, e.g., `(-priority, item)`, ensure the `item` is comparable in case priorities tie).*

---

## Time and Space Complexity

- **Heapify**: $O(N)$
- **Push**: $O(\log N)$
- **Pop**: $O(\log N)$
- **Peek Minimum**: $O(1)$ (using `heap[0]`)

---

## Summary
- A Heap instantly provides the Min/Max element.
- Python's `heapq` uses standard lists and only provides a **Min-Heap**.
- For a Max-Heap, insert `-value`.
- Use a Min-Heap of size $K$ to solve "Top K Largest" problems in $O(N \log K)$ time.
