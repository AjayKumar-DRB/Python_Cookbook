# Union-Find (Disjoint Set)

## Introduction

Union-Find (also known as Disjoint Set Union or DSU) is a data structure used exclusively to keep track of a set of elements partitioned into a number of disjoint (non-overlapping) subsets.

It answers two questions incredibly quickly (nearly $O(1)$ time):
1. **Find**: Which set does this element belong to?
2. **Union**: Merge two sets together.

---

## How to Recognize It

Use Union-Find when:
- The problem involves finding **Connected Components** in an undirected graph.
- You need to determine if adding an edge will create a **Cycle**.
- You are implementing Kruskal's Algorithm for Minimum Spanning Trees.
- The problem describes establishing connections between items (e.g., "Friend Circles", "Redundant Connection").

---

## The Core Concept

Imagine every node starts as its own independent set (a "parent" of itself).

When we **Union** two nodes $A$ and $B$, we find their respective "root" parents. We then make the root of $A$ point to the root of $B$. Now they belong to the same set.

To keep the trees extremely flat and fast, we use two optimizations:
1. **Path Compression**: When finding the root of $A$, we make every node along the path point directly to the root.
2. **Union by Rank (or Size)**: When merging two sets, we attach the smaller tree to the root of the larger tree.

---

## The Pythonic Implementation

You can implement Union-Find using a simple array where `parent[i]` stores the parent of node `i`.

```python
class UnionFind:
    def __init__(self, size):
        # Initially, each node is its own parent
        self.parent = list(range(size))
        # Rank tracks the depth of the tree to optimize merges
        self.rank = [1] * size
        self.components = size

    def find(self, i):
        # Path Compression
        if self.parent[i] != i:
            # Recursively find the root and compress the path
            self.parent[i] = self.find(self.parent[i])
        return self.parent[i]

    def union(self, i, j):
        root_i = self.find(i)
        root_j = self.find(j)

        if root_i == root_j:
            return False # They are already in the same set! (Cycle detected)

        # Union by Rank
        if self.rank[root_i] > self.rank[root_j]:
            self.parent[root_j] = root_i
        elif self.rank[root_i] < self.rank[root_j]:
            self.parent[root_i] = root_j
        else:
            self.parent[root_j] = root_i
            self.rank[root_i] += 1
            
        self.components -= 1
        return True
```

---

## Example: Redundant Connection

Given an undirected graph, return an edge that can be removed to make the graph a tree (i.e., remove the edge that forms a cycle).

```python
def find_redundant_connection(edges):
    # Graph has N nodes labeled 1 to N
    uf = UnionFind(len(edges) + 1)
    
    for u, v in edges:
        # If union returns False, u and v are already connected!
        # Therefore, this edge (u, v) is the one creating the cycle.
        if not uf.union(u, v):
            return [u, v]
            
    return []
```

---

## Time and Space Complexity

Let $N$ be the number of nodes.
- **Time Complexity**: $O(\alpha(N))$ for both Find and Union operations, where $\alpha$ is the Inverse Ackermann function. For all practical purposes in the universe, $\alpha(N) \le 4$. Therefore, operations take **amortized $O(1)$ time**.
- **Space Complexity**: $O(N)$ to store the `parent` and `rank` arrays.

---

## Summary
- Use Union-Find for **Connected Components** and **Cycle Detection** in undirected graphs.
- Memorize the `find` function with **Path Compression**.
- Memorize the `union` function with **Union by Rank**.
