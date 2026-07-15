# Monotonic Queue

## Introduction

A Monotonic Queue is a variation of the Monotonic Stack, but implemented using a `deque` (double-ended queue).

It is used specifically for finding the **Maximum or Minimum element in a Sliding Window** in $O(N)$ time.

---

## How to Recognize It

Use a Monotonic Queue when:
- The problem is explicitly "Sliding Window Maximum" (LeetCode 239).
- You are doing Dynamic Programming where the state transition looks back at a specific window of previous states and needs the maximum/minimum among them (e.g., Jump Game VI).

---

## The Core Concept

Imagine a sliding window moving across an array, and you need the maximum value in that window. 

A Monotonic Queue stores indices, and ensures that the values corresponding to those indices are strictly decreasing. Therefore, the **front of the queue always contains the index of the maximum value**.

When a new element arrives:
1. **Maintain Window bounds**: If the index at the front of the queue falls outside the current sliding window, `popleft()` it.
2. **Maintain Monotonicity**: While the new element is *greater* than the elements at the back of the queue, those older, smaller elements can *never* be the maximum in the future. So, `pop()` them from the back.
3. **Add**: Append the new element's index to the back.

### Example: Sliding Window Maximum

```python
from collections import deque

def max_sliding_window(nums, k):
    result = []
    # Stores indices, values at indices are strictly decreasing
    queue = deque() 
    
    for i, num in enumerate(nums):
        
        # 1. Remove indices that are out of the current window
        # The window spans from (i - k + 1) to i.
        if queue and queue[0] < i - k + 1:
            queue.popleft()
            
        # 2. Remove smaller elements from the back
        # They are useless because 'num' is larger and arrived later
        while queue and nums[queue[-1]] <= num:
            queue.pop()
            
        # 3. Add current index to the back
        queue.append(i)
        
        # 4. If our window has hit size k, record the max
        if i >= k - 1:
            result.append(nums[queue[0]]) # Front is always max
            
    return result
```

---

## Time and Space Complexity

- **Time Complexity**: $O(N)$. Just like the Monotonic Stack, every index is pushed to the deque exactly once and popped at most once.
- **Space Complexity**: $O(K)$. The queue never stores more than $K$ indices at a time.

---

## Summary
- Use a Monotonic Queue (via `collections.deque`) for "Sliding Window Maximum/Minimum" problems.
- Store **indices** in the deque.
- `popleft()` indices that fall out of the window.
- `pop()` from the right if the incoming element invalidates older elements.
- The front of the queue `queue[0]` always holds the max/min.
