# Trees

## Introduction

A Tree is a hierarchical data structure. In interviews, 95% of tree problems involve **Binary Trees**, where each node has at most two children (left and right).

---

## The Standard `TreeNode`

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

---

## Depth-First Search (DFS)

DFS goes as deep as possible down one path before backtracking. It is almost always implemented **recursively**.

DFS is used when a problem asks about tree depth, path sums, or requires validating the structure (like checking if two trees are identical).

### The 3 Traversal Orders
Depending on when you process the current node's value, DFS has three variations:

1. **Pre-order (Node, Left, Right)**: Useful for copying a tree.
2. **In-order (Left, Node, Right)**: Crucial for Binary Search Trees (it visits nodes in sorted order).
3. **Post-order (Left, Right, Node)**: Useful for deleting a tree or when you need information from children before evaluating the parent (e.g., calculating tree height).

### DFS Recursive Template

```python
def dfs(node):
    # 1. Base case (critical to prevent infinite recursion)
    if not node:
        return
        
    # Pre-order logic goes here
    
    dfs(node.left)
    
    # In-order logic goes here
    
    dfs(node.right)
    
    # Post-order logic goes here
```

---

## Breadth-First Search (BFS)

BFS explores the tree level by level. It is implemented iteratively using a **Queue**.

BFS is used when a problem explicitly mentions "levels" (e.g., Level Order Traversal, Right Side View) or asks for the **shortest path** in an unweighted tree/graph.

### BFS Iterative Template

```python
from collections import deque

def bfs(root):
    if not root:
        return []
        
    queue = deque([root])
    
    while queue:
        # Get the number of nodes at the current level
        level_size = len(queue)
        
        for _ in range(level_size):
            node = queue.popleft()
            
            # Process node
            print(node.val)
            
            # Add children for the next level
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
```
*(Note: Capturing `level_size` before the `for` loop is the secret to knowing exactly which nodes belong to the current level, as the queue size will change during the loop).*

---

## Time and Space Complexity

For a tree with $N$ nodes and height $H$:
- **Time Complexity (DFS & BFS)**: $O(N)$ because you must visit every node.
- **Space Complexity (DFS)**: $O(H)$ due to the call stack. In the worst case (a skewed tree), $H = N$. In a balanced tree, $H = \log N$.
- **Space Complexity (BFS)**: $O(W)$ where $W$ is the maximum width of the tree. In a balanced tree, the bottom level has $N/2$ nodes, so worst-case space is $O(N)$.

---

## Summary
- Use **DFS (Recursion)** for paths, depths, and bottom-up calculations (Post-order).
- Use **BFS (Queue)** for level-by-level traversal and shortest paths.
- For BFS, capture `level_size = len(queue)` to process nodes level by level.
- Always include the base case `if not node: return` to prevent recursion crashes.
