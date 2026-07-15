# Medium Roadmap

> The core of FAANG interviews.

---

## Introduction

"Medium" LeetCode questions make up roughly 80% of the questions asked in FAANG onsite interviews. 

They are the perfect balance: they require you to combine 2 or 3 fundamental concepts from the Easy tier, but they don't require obscure, esoteric algorithms.

---

## The Goals of Medium Questions

1. **Pattern Recognition:** You read a prompt and immediately know it's a "Sliding Window" or "Topological Sort" problem.
2. **Trade-off Analysis:** You can discuss whether to optimize for Time or Space.
3. **Graph and Tree Mastery:** You are completely comfortable traversing complex non-linear structures.

---

## The Medium Patterns to Master

You should spend the vast majority of your prep time here. Aim to solve these in 20-30 minutes.

### 1. Sliding Window
Maintaining a dynamic subset of contiguous elements.
- **Classic Problem:** Longest Substring Without Repeating Characters (LeetCode 3)
- **Classic Problem:** Best Time to Buy and Sell Stock (LeetCode 121 - Note: technically easy, but sliding window concept)

### 2. Fast & Slow Pointers (Floyd's Tortoise and Hare)
Using pointers that move at different speeds to find cycles or midpoints.
- **Classic Problem:** Linked List Cycle (LeetCode 141)
- **Classic Problem:** Find the Duplicate Number (LeetCode 287)

### 3. Backtracking
Generating combinations, permutations, and subsets by exploring and undoing state.
- **Classic Problem:** Subsets (LeetCode 78)
- **Classic Problem:** Combination Sum (LeetCode 39)

### 4. Graph Traversals (BFS & DFS on Matrices)
Treating a 2D grid as a graph and exploring islands or paths.
- **Classic Problem:** Number of Islands (LeetCode 200)
- **Classic Problem:** Rotting Oranges (LeetCode 994)

### 5. Top K Elements (Heaps)
Using a Priority Queue to maintain the largest or smallest elements efficiently.
- **Classic Problem:** Top K Frequent Elements (LeetCode 347)
- **Classic Problem:** Kth Largest Element in an Array (LeetCode 215)

### 6. Intervals
Sorting arrays of start/end times and merging overlapping segments.
- **Classic Problem:** Merge Intervals (LeetCode 56)
- **Classic Problem:** Insert Interval (LeetCode 57)

### 7. 1D Dynamic Programming
Caching overlapping subproblems in an array (Tabulation) or Dictionary (Memoization).
- **Classic Problem:** Climbing Stairs (LeetCode 70)
- **Classic Problem:** Coin Change (LeetCode 322)

---

## When are you ready for Hards?

You are ready for Hards when:
- You can implement BFS and DFS on a matrix in under 5 minutes without thinking.
- You can write a standard Backtracking template perfectly from memory.
- You immediately recognize when to use a Heap vs sorting the entire array.

---

## Related Topics

- [Hard Roadmap](04-hard-roadmap.md)
- [NeetCode 150](06-neetcode-150.md)
