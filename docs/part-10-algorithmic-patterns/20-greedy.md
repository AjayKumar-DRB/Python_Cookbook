# Greedy Algorithms

## Introduction

A Greedy Algorithm builds up a solution piece by piece, always choosing the next piece that offers the most obvious and immediate benefit (the "local optimum").

Greedy algorithms do not look ahead to see if a choice will hurt them in the long run. 

---

## How to Recognize It

Greedy algorithms are notoriously difficult to prove correct during an interview. They are typically used when:
- The problem asks for a minimum/maximum result (similar to DP).
- The choices are independent, or the optimal local choice mathematically guarantees the optimal global result.
- A DP solution exists, but the constraints are massive (e.g., $N = 10^5$), implying an $O(N \log N)$ or $O(N)$ solution is required.

---

## When Greedy works (and when it fails)

Consider the "Coin Change" problem: Find the minimum number of coins to make `amount` using a given set of `coins`.

**Case 1: Standard US Coins (1, 5, 10, 25)**
If you want to make 30 cents, a Greedy approach works: Take the biggest coin possible (25), leaving 5. Take the biggest coin (5), leaving 0. Total = 2 coins.

**Case 2: Custom Coins (1, 3, 4)**
If you want to make 6 cents, a Greedy approach fails: Take the biggest (4), leaving 2. Take two 1s. Total = 3 coins. 
But the optimal answer is two 3s (Total = 2 coins).

This is why Greedy is dangerous. If you cannot mathematically prove that taking the local optimum is always safe, you must use Dynamic Programming.

---

## Common Greedy Patterns

### 1. Sorting First
Almost all greedy algorithms start by sorting the input. Sorting allows you to process items in their optimal order (e.g., largest to smallest).

**Example: Jump Game (LeetCode 55)**
Determine if you can reach the last index of an array.
Instead of exploring all paths (DFS/DP), just track the `farthest_reachable` index.

```python
def can_jump(nums):
    farthest_reachable = 0
    
    for i in range(len(nums)):
        # If the current index is beyond our farthest reach, we are stuck
        if i > farthest_reachable:
            return False
            
        # Update our farthest reach from this index
        farthest_reachable = max(farthest_reachable, i + nums[i])
        
        # If we can reach the end, success
        if farthest_reachable >= len(nums) - 1:
            return True
            
    return True
```

### 2. Intervals / Scheduling
Greedy is heavily used in interval scheduling (e.g., "Find the maximum number of non-overlapping meetings you can attend").
**The Greedy Choice**: Always pick the meeting that **ends the earliest**. (Sort by end time!).

```python
def max_events(intervals):
    if not intervals: return 0
    
    # Sort by END time
    intervals.sort(key=lambda x: x[1])
    
    count = 1
    last_end = intervals[0][1]
    
    for i in range(1, len(intervals)):
        start, end = intervals[i]
        # If this event starts after the last one ended, we can attend
        if start >= last_end:
            count += 1
            last_end = end
            
    return count
```

---

## Summary
- Greedy algorithms pick the best immediate choice.
- They are highly efficient ($O(N \log N)$ with sorting, or $O(N)$ linear scans).
- Be careful: they do not work for all optimization problems (like general Coin Change or Knapsack problems). Use DP for those.
- Common trigger: "Max overlapping intervals" or "Activity Selection".
