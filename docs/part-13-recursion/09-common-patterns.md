# Common Recursion Patterns

> Standardizing the way you write recursion saves time in interviews.

---

## Introduction

Recursion can feel incredibly open-ended. However, in coding interviews, almost all recursive problems fall into one of two patterns: **Top-Down** or **Bottom-Up**.

Understanding these two patterns will help you structure your code instantly when you encounter a new problem.

---

## 1. Top-Down (Passing state down)

In the Top-Down pattern, the parent function computes some state and passes it down to its children as arguments. 

Think of this as: *"I am doing the work, and passing the results downwards."*

**Example: Finding the maximum depth of a binary tree (Top-Down)**
```python
ans = 0

def top_down_depth(root, current_depth):
    global ans
    if not root:
        return
        
    # Update the global answer if the current depth is greater
    ans = max(ans, current_depth)
    
    # Pass the updated state down to the children
    top_down_depth(root.left, current_depth + 1)
    top_down_depth(root.right, current_depth + 1)

top_down_depth(root, 1)
return ans
```

### Characteristics of Top-Down:
- Often relies on a global or non-local variable to store the final answer.
- The recursive function usually returns `None`.
- It acts similarly to a Pre-Order traversal.

---

## 2. Bottom-Up (Returning state up)

In the Bottom-Up pattern, the parent function relies entirely on the return values of its children to compute its own answer. 

Think of this as: *"I will wait for my children to give me their answers, and then I will combine them."*

**Example: Finding the maximum depth of a binary tree (Bottom-Up)**
```python
def bottom_up_depth(root):
    if not root:
        return 0
        
    # Wait for the children to return their answers
    left_depth = bottom_up_depth(root.left)
    right_depth = bottom_up_depth(root.right)
    
    # Combine the answers and pass them back up
    return max(left_depth, right_depth) + 1

return bottom_up_depth(root)
```

### Characteristics of Bottom-Up:
- The recursive function explicitly returns a value.
- No global variables are needed; the answer bubbles up to the root.
- It acts similarly to a Post-Order traversal.
- This is generally considered cleaner and more "functional" than Top-Down.

---

## 3. The "Helper Function" Pattern

A very common pattern in Python is defining a nested recursive helper function inside the main function. 

This is incredibly useful because the inner function can access variables in the outer function's scope, avoiding the need for messy `global` keywords or passing massive arrays through every recursive call.

```python
def subsets(nums):
    res = []
    subset = []
    
    # The helper function has access to `res`, `subset`, and `nums` implicitly!
    def dfs(i):
        if i >= len(nums):
            res.append(subset.copy())
            return
            
        # Include nums[i]
        subset.append(nums[i])
        dfs(i + 1)
        
        # Don't include nums[i]
        subset.pop()
        dfs(i + 1)
        
    dfs(0)
    return res
```

---

## Best Practices

- Prefer **Bottom-Up** recursion when possible, as returning values is generally cleaner than mutating global state.
- Use the **Helper Function** pattern for backtracking or DFS, as it cleanly encapsulates the recursion without polluting the global scope.

---

## Related Topics

- [Recursion Basics](02-recursion-basics.md)
- [Trees](../part-10-algorithmic-patterns/14-trees.md)
