# Standard Library Interview Recipes

## Introduction

Memorize these recipes to dramatically reduce the amount of code you need to write during an interview. They cover the most common patterns involving heaps, caching, and combinatorics.

---

## Recipe 1: Top K Elements (Min-Heap)

When asked to find the Top K largest elements, use a Min-Heap of size K. Iterate through the array, pushing elements onto the heap. If the heap size exceeds K, pop the smallest element.

```python
import heapq

def top_k_largest(nums, k):
    min_heap = []
    
    for num in nums:
        heapq.heappush(min_heap, num)
        if len(min_heap) > k:
            # Removes the smallest element in the heap
            heapq.heappop(min_heap)
            
    # The heap now contains the K largest elements
    return min_heap
```
- **Time Complexity**: $O(N \log K)$
- **Space Complexity**: $O(K)$

---

## Recipe 2: Top-Down DP with `@cache`

When solving a dynamic programming problem using recursion, avoid writing manual `memo` dictionaries. Import `lru_cache` or `cache`.

```python
from functools import cache

def climb_stairs(n):
    @cache # Automatically memoizes inputs
    def dp(steps_left):
        if steps_left == 0:
            return 1
        if steps_left < 0:
            return 0
            
        return dp(steps_left - 1) + dp(steps_left - 2)
        
    return dp(n)
```
- **Crucial Rule**: Ensure all arguments to `dp()` are immutable (e.g., use tuples, not lists).

---

## Recipe 3: Checking Existence in a Sorted Array

If an array is already sorted and you need to check if a specific target exists, use `bisect_left`.

```python
import bisect

def exists(nums, target):
    # Find where the target SHOULD go
    idx = bisect.bisect_left(nums, target)
    
    # Check if it actually exists at that index
    return idx < len(nums) and nums[idx] == target
```
- **Time Complexity**: $O(\log N)$

---

## Recipe 4: Generating All Subsets (Power Set)

While you should know how to do this with backtracking, if the interviewer allows standard library tools, `itertools.combinations` is the fastest way to generate a power set.

```python
import itertools

def generate_subsets(nums):
    result = []
    for length in range(len(nums) + 1):
        # Generate combinations for each possible length
        for combo in itertools.combinations(nums, length):
            result.append(list(combo))
    return result
```

---

## Summary
- **Top K**: Iterate and maintain a `heapq` of size K.
- **DP**: Use `@cache` on inner recursive functions.
- **Binary Search**: Use `bisect_left(arr, target)`.
- **Combinatorics**: Use `itertools.combinations` to generate subsets without backtracking.
