# Breadth-First Search (BFS) Template

## The Template

```python
from collections import deque

def bfs(root):
    # Base case check
    if not root:
        return []
        
    queue = deque([root])
    # visited = set([root]) # Only needed for Graphs, NOT Trees!
    
    steps = 0 # Track distance/levels
    
    while queue:
        # Snap the size to process exactly one "level" at a time
        level_size = len(queue)
        
        for _ in range(level_size):
            node = queue.popleft()
            
            # PROCESS NODE HERE
            print(node.val)
            
            # Add valid neighbors/children to the queue
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
                
        # Increment step count after completing a full level
        steps += 1
        
    return steps
```

## Crucial Reminders
1. **Always use `collections.deque`**. Never use a list `pop(0)`, which is $O(N)$ and will fail performance tests.
2. **The `level_size` trick**: If the problem asks for the "shortest path" or to group nodes by "level" (e.g., Binary Tree Level Order Traversal), you MUST capture `level_size = len(queue)` before the `for` loop. If you just `popleft()` without the nested `for` loop, you lose track of which nodes belong to which distance level.
3. **Graphs vs Trees**: Trees do not have cycles, so a `visited` set is not needed. If doing BFS on a Graph, you MUST add nodes to a `visited` set **the exact moment you append them to the queue** (not when you pop them), to prevent adding the same node multiple times.
