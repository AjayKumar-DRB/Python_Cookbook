# Identifying Patterns

> Step 2: Match.

---

## Introduction

Once you understand the problem and the constraints, you must match it to a known algorithmic pattern. 

You should rarely invent a brand new algorithm in an interview. Almost every FAANG question is a variation of one of $\approx 15$ core patterns.

---

## How to Match a Pattern

Look for keywords or structural hints in the prompt.

### 1. "Top K", "Kth largest", "K closest"
**Pattern:** Heap (Priority Queue) or Quickselect.
**Why:** Heaps are perfectly designed to maintain a running top K elements in $O(N \log K)$ time.

### 2. "Sorted array", "Find a target", "$O(\log N)$ required"
**Pattern:** Binary Search.
**Why:** Binary search is the only way to search an array in $O(\log N)$.

### 3. "Subarray", "Contiguous sequence", "Longest/Shortest substring"
**Pattern:** Sliding Window.
**Why:** Sliding window processes contiguous elements in $O(N)$ time by expanding and shrinking bounds.

### 4. "All combinations", "All permutations", "Generate all"
**Pattern:** Backtracking.
**Why:** Backtracking systematically explores a decision tree to generate exhaustive possibilities.

### 5. "Shortest path", "Minimum steps to reach"
**Pattern:** Breadth-First Search (BFS).
**Why:** BFS explores uniformly in all directions, guaranteeing the first time you hit the target is the shortest path.

### 6. "Connectivity", "Islands", "Explore all connected nodes"
**Pattern:** Depth-First Search (DFS) or Union Find.
**Why:** DFS fully explores a connected component easily.

### 7. "Maximum/Minimum ways to do X", "Optimal sub-structure"
**Pattern:** Dynamic Programming.
**Why:** When the answer to a large problem depends on the optimal answers to smaller subproblems, DP (Memoization/Tabulation) is required to avoid recalculating overlapping states.

### 8. "Find pairs", "Two numbers sum to X"
**Pattern:** Two Pointers or HashMap.
**Why:** If sorted, Two Pointers works in $O(N)$. If unsorted, a HashMap works in $O(N)$ time and space.

### 9. "Next Greater Element", "Daily Temperatures"
**Pattern:** Monotonic Stack.
**Why:** Maintaining a strictly increasing or decreasing stack is the optimal way to resolve "next greater/smaller" queries in $O(N)$ time.

---

## What if no pattern matches?

If the problem doesn't clearly fit any of the above:
1. **Try sorting the data.** Does sorting it reveal a pattern?
2. **Try a Greedy approach.** Can you make a locally optimal choice at each step?
3. **Try Brute Force.** Write out the naive $O(N^2)$ or $O(2^N)$ approach. Sometimes, writing the brute force makes the optimal pattern obvious (e.g., realizing you are doing redundant work, leading to DP).

---

## Key Takeaways

- Memorize the keywords associated with each pattern.
- The vast majority of interview questions are just dressed-up versions of these patterns.
- If stuck, think: *Would sorting help? Can I use a HashMap?*

---

## Related Topics

- [Choosing Data Structures](04-choosing-data-structures.md)
- [LeetCode Patterns](../part-17-leetcode-patterns/01-index.md)
