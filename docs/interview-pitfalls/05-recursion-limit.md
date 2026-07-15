# Recursion Limits

## The Pitfall

Unlike languages like C++ or Java, Python is heavily guarded against infinite recursion to prevent stack overflows that crash the CPython interpreter.

By default, Python sets a strict maximum recursion depth (usually 1,000 calls). 

If your algorithm recurses more than 1,000 times, Python will throw a `RecursionError: maximum recursion depth exceeded`.

---

## When Does This Happen?

This rarely happens in balanced Tree problems, because a tree with a depth of 1,000 would contain $2^{1000}$ nodes.

However, it happens very frequently in:
1. **Graphs (DFS)**: If a graph is essentially a long straight line of 10,000 nodes, a recursive DFS will crash.
2. **Linked Lists**: Reversing a Linked List of 10,000 nodes recursively will crash.
3. **Dynamic Programming**: Top-Down DP on a string of length 2,000 will crash.

---

## The Fixes

### 1. The Interviewer's Fix (Iteration)
If the interviewer asks, "How would you handle a massive input that causes a stack overflow?", the correct theoretical answer is to **rewrite the algorithm iteratively**.
- Replace recursive DFS with an explicit `stack` (a simple array).
- Replace Top-Down DP with Bottom-Up Tabulation (a `for` loop).

### 2. The Competitive Programming Fix (Sys Module)
If you are taking an automated online assessment (HackerRank, CodeSignal) and your recursive solution fails on hidden test cases due to `RecursionError`, you can manually increase the limit.

```python
import sys
sys.setrecursionlimit(20000) # Increase limit to 20,000
```
*(Warning: Only use this in automated tests. If you do this in a live interview, the interviewer will likely view it as a hack and ask you to rewrite it iteratively).*
