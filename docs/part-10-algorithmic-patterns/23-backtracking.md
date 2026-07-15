# Backtracking

## Introduction

Backtracking is an algorithmic paradigm for finding all (or some) solutions to computational problems by incrementally building candidates, and abandoning a candidate ("backtracking") as soon as it determines that the candidate cannot lead to a valid solution.

---

## How to Recognize It

Use Backtracking when:
- The problem asks for **"All permutations"**, **"All combinations"**, or **"All subsets"**.
- The problem asks you to generate all valid configurations (e.g., N-Queens, Sudoku, Generate Parentheses).

---

## The Core Concept (DFS on a Decision Tree)

Backtracking is fundamentally a Depth-First Search (DFS) on a tree of decisions.

At every step, you:
1. **Choose**: Add a candidate to your current path.
2. **Explore**: Recursively call DFS to continue building from this path.
3. **Un-Choose (Backtrack)**: Remove the candidate from your path and try the next option.

---

## The Standard Template

```python
def solve_backtracking(nums):
    result = []
    
    def backtrack(start_index, current_path):
        # 1. Base Case: Have we reached a valid solution?
        # (e.g., path length equals required length)
        if is_valid_solution(current_path):
            # Must append a COPY of the path!
            result.append(list(current_path)) 
            return # Sometimes return, sometimes continue exploring
            
        # 2. Iterate through all possible choices at this step
        for i in range(start_index, len(nums)):
            
            # (Optional) Pruning: Skip invalid choices
            if not is_valid_choice(nums[i]):
                continue
                
            # 3. CHOOSE
            current_path.append(nums[i])
            
            # 4. EXPLORE
            # Depending on the problem, the next start index might be i or i+1
            backtrack(i + 1, current_path)
            
            # 5. UN-CHOOSE (Backtrack)
            current_path.pop()
            
    backtrack(0, [])
    return result
```

---

## Crucial Pitfall: Appending References

The most common bug in a backtracking interview is appending the reference of `current_path` to the `result` array.

```python
# WRONG
result.append(current_path) 
```

Because lists in Python are mutable, if you append the reference, any future `pop()` or `append()` operations will modify the list *already stored in the result*. At the end, your result will be full of empty arrays!

**Always append a shallow copy.**
```python
# RIGHT
result.append(list(current_path)) 
# or
result.append(current_path[:])
```

---

## Time and Space Complexity

Backtracking algorithms are essentially brute-force, so their time complexities are massive.

- **Permutations Time Complexity**: $O(N \times N!)$
- **Combinations/Subsets Time Complexity**: $O(N \times 2^N)$
- **Space Complexity**: $O(N)$ for the recursion stack and the `current_path` list (excluding the memory required to hold the `result`).

---

## Summary
- Backtracking is DFS applied to decision trees.
- The lifecycle: `Choose -> Explore -> Un-choose`.
- **Always append a copy** of the path to the results array (`list(path)`).
- Time complexity is exponential ($O(2^N)$) or factorial ($O(N!)$).
