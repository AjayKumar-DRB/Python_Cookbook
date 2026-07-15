# Shallow vs Deep Copy

## The Pitfall

In Python, assignment (`=`) never copies data. It only binds a new name to the existing object. 
If the object is mutable (like a list), modifying it through one name modifies it for all names.

This causes two massive bugs in interviews: Matrix Initialization and Backtracking results.

---

## Bug 1: The 2D Matrix Trap

You are starting a Dynamic Programming problem, so you initialize a grid of zeros.

```python
# The Broken Code
ROWS, COLS = 3, 3
grid = [[0] * COLS] * ROWS

# Let's set the top-left cell to 1
grid[0][0] = 1

print(grid)
```

**What you expect:**
```python
[[1, 0, 0], 
 [0, 0, 0], 
 [0, 0, 0]]
```

**What actually happens:**
```python
[[1, 0, 0], 
 [1, 0, 0], 
 [1, 0, 0]]
```

**Why?**
The `* ROWS` operation duplicated the *reference* to the inner list. `grid[0]`, `grid[1]`, and `grid[2]` are all pointing to the exact same list in memory.

**The Fix:**
Use a list comprehension to force Python to create a new list for every row.
```python
grid = [[0] * COLS for _ in range(ROWS)]
```

---

## Bug 2: The Backtracking Trap

You are writing a Backtracking algorithm to find all valid combinations. When you find a valid path, you append it to the result array.

```python
# The Broken Code
result = []

def backtrack(path):
    if len(path) == 3:
        result.append(path) # DANGER!
        return
        
    for i in range(1, 4):
        path.append(i)
        backtrack(path)
        path.pop() # Un-choose

backtrack([])
print(result)
```

**What you expect:**
```python
[[1, 2, 3], [1, 3, 2], ...]
```

**What actually happens:**
```python
[[], [], [], [], ...]
```

**Why?**
You appended a *reference* to the `path` list. As the backtracking algorithm continued, it eventually popped every element out of `path`. Because the `result` array holds references to that same list, all the lists inside `result` appear empty.

**The Fix:**
Always append a shallow copy of the list.
```python
result.append(list(path))
# OR
result.append(path[:])
```
