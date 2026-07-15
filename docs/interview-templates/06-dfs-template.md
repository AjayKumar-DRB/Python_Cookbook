# Depth-First Search (DFS) / Backtracking Template

## Template 1: Tree Traversal

```python
def dfs_tree(node):
    # 1. Base Case
    if not node:
        return
        
    # PRE-ORDER logic (e.g., append to path)
    
    dfs_tree(node.left)
    
    # IN-ORDER logic (e.g., validate BST)
    
    dfs_tree(node.right)
    
    # POST-ORDER logic (e.g., calculate tree height)
```

## Template 2: Backtracking (Combinations/Permutations)

```python
def solve_backtracking(options):
    result = []
    
    def backtrack(start_index, current_path):
        # 1. Goal Check
        if is_goal(current_path):
            result.append(list(current_path)) # MUST APPEND A COPY
            return
            
        # 2. Iterate Choices
        for i in range(start_index, len(options)):
            # Prune invalid choices
            if not is_valid(options[i]):
                continue
                
            # 3. Choose
            current_path.append(options[i])
            
            # 4. Explore
            backtrack(i + 1, current_path) # Pass 'i' if reusing elements is allowed
            
            # 5. Un-choose
            current_path.pop()
            
    backtrack(0, [])
    return result
```

## Crucial Reminders
1. **Base Cases First**: Always check `if not node:` before attempting to access `.left` or `.right`.
2. **Shallow Copies**: In backtracking, `result.append(path)` will fail because `path` is a reference to a mutable list that you will `pop()` later. Always use `list(path)` or `path[:]`.
3. **Start Index**: If finding Combinations, pass `i + 1` to the recursive call to prevent duplicates. If finding Permutations, you usually iterate from `0` to `N` and use a `visited` set to skip elements already in the path.
