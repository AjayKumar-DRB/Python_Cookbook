# Hard Roadmap

> The differentiator for Senior/Staff roles.

---

## Introduction

"Hard" LeetCode questions are rarely asked for entry-level or junior roles, but they are increasingly common for Senior, Staff, or highly competitive Quantitative Finance roles.

Hard questions are usually one of two things:
1. Two completely different Medium patterns chained together.
2. A single extremely obscure algorithm (like A*, Kosaraju's, or complex Bitmask DP).

---

## The Goals of Hard Questions

1. **Managing Complexity:** Writing 60-100 lines of bug-free code without losing track of your state.
2. **Advanced Data Structures:** Using Segment Trees, Tries, or Disjoint Sets (Union Find).
3. **Advanced Optimization:** Reducing $O(N^2)$ to $O(N \log N)$ or $O(N)$ using Monotonic Stacks or Deques.

---

## The Hard Patterns to Master

Only study these if you are consistently crushing Mediums.

### 1. Monotonic Stack
Maintaining a strictly increasing or decreasing stack to find the "Next Greater Element" in $O(N)$ time.
- **Classic Problem:** Trapping Rain Water (LeetCode 42)
- **Classic Problem:** Largest Rectangle in Histogram (LeetCode 84)

### 2. Union Find (Disjoint Set)
Finding connected components and cycles in undirected graphs efficiently.
- **Classic Problem:** Redundant Connection (LeetCode 684)
- **Classic Problem:** Number of Connected Components in an Undirected Graph (LeetCode 323)

### 3. Tries (Prefix Trees)
Storing strings character-by-character for lightning-fast prefix lookups.
- **Classic Problem:** Implement Trie (LeetCode 208)
- **Classic Problem:** Word Search II (LeetCode 212) - *Combines Trie with Matrix DFS!*

### 4. Advanced Graph Algorithms (Dijkstra / Topological Sort)
Finding shortest paths in weighted graphs, or ordering graphs with dependencies.
- **Classic Problem:** Network Delay Time (LeetCode 743) - *Dijkstra's*
- **Classic Problem:** Alien Dictionary (LeetCode 269) - *Topological Sort*

### 5. 2D Dynamic Programming
State depends on two changing variables (usually represented by a 2D matrix).
- **Classic Problem:** Longest Common Subsequence (LeetCode 1143)
- **Classic Problem:** Edit Distance (LeetCode 72)

### 6. Median / Sliding Window Heaps
Using TWO heaps (a Max Heap and a Min Heap) simultaneously.
- **Classic Problem:** Find Median from Data Stream (LeetCode 295)
- **Classic Problem:** Sliding Window Maximum (LeetCode 239)

---

## The Reality of Hard Questions

If you get a Hard question in an interview, the interviewer is often testing your **problem-solving resilience** more than your memorization. 

They expect you to struggle. They expect to give you hints. 
If you communicate clearly, implement a solid brute-force, and work collaboratively with them to optimize it using a complex pattern, you will pass.

---

## Key Takeaways

- Hards often combine two Medium patterns.
- Master Monotonic Stacks and Union Find.
- Do not let a Hard question panic you; communicate and build up from the brute force.

---

## Related Topics

- [Medium Roadmap](03-medium-roadmap.md)
- [Company Patterns](08-company-patterns.md)
