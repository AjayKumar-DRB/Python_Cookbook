# LeetCode Pattern Recipes

> How to quickly identify the pattern during an interview.

---

## Keyword Identification Guide

If you hear these words in an interview prompt, immediately consider the associated pattern.

| If you hear... | Think... | Time Complexity |
|----------------|----------|-----------------|
| "Sorted array", "Find target in $O(\log N)$" | **Binary Search** | $O(\log N)$ |
| "Top K", "Kth Largest/Smallest" | **Heap (Priority Queue)** | $O(N \log K)$ |
| "Contiguous Subarray", "Longest substring" | **Sliding Window** | $O(N)$ |
| "Pairs that sum to X", "Reverse an array" | **Two Pointers** | $O(N)$ |
| "Find all combinations/permutations" | **Backtracking** | $O(2^N)$ or $O(N!)$ |
| "Shortest path", "Minimum steps" | **BFS (Queue)** | $O(V + E)$ |
| "Connected components", "Islands", "Explore all" | **DFS (Stack/Recursion)** | $O(V + E)$ |
| "Next greater element", "Daily Temperatures" | **Monotonic Stack** | $O(N)$ |
| "Max/Min ways to reach state", "Overlapping subproblems" | **Dynamic Programming** | Varies (often $O(N^2)$) |
| "Prefix matching", "Autocomplete" | **Trie (Prefix Tree)** | $O(L)$ per word |
| "Cycle in an undirected graph", "Grouping sets" | **Union Find (Disjoint Set)** | $O(V + E \alpha(V))$ |

---

## The "Sorting" Shortcut

If you are completely stuck on an Array or String problem, ask yourself:
*"Does the output require the original indices?"*

- If **YES** (e.g., Two Sum where you must return indices `[0, 1]`): You **cannot** sort the array. You must use a Hash Map or extra space.
- If **NO** (e.g., Find if a subset exists, return the values): **Try sorting the array first!** Sorting takes $O(N \log N)$ and almost always unlocks a Two Pointer or Binary Search solution that uses $O(1)$ space.

---

## The "Graph" Shortcut

Sometimes a problem doesn't look like a graph, but it is.
- If it's a 2D Matrix (Grid) where you can move up/down/left/right -> It's a Graph.
- If it's a list of prerequisites (e.g., "Course A must be taken before Course B") -> It's a Directed Graph (Topological Sort).
- If it's a list of connected flights or friends -> It's a Graph.

Whenever you realize it's a graph, immediately write down the Adjacency List template:
```python
adj = collections.defaultdict(list)
for u, v in edges:
    adj[u].append(v)
    adj[v].append(u) # If undirected
```

---

## Key Takeaways

- Memorize the keywords that map to patterns.
- Sorting is the most powerful tool for solving array problems when original indices don't matter.
- Many word or grid problems are just hidden Graph traversals.
