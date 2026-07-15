# Multidimensional Lists (Matrices)

## Introduction

In Python, a 2D array (matrix) is simply a list of lists. 

You will use 2D lists heavily in Graph problems (adjacency matrices), Dynamic Programming (2D memoization tables), and Grid traversal problems (like Islands or Mazes).

---

## The Danger of `[[0] * C] * R`

The most common bug in Python coding interviews is initializing a 2D matrix incorrectly.

**❌ Incorrect Initialization:**
```python
R, C = 3, 3
matrix = [[0] * C] * R
```
If you print `matrix`, it looks correct:
`[[0, 0, 0], [0, 0, 0], [0, 0, 0]]`

But if you modify one element:
```python
matrix[0][0] = 1
print(matrix)
```
**Output:**
`[[1, 0, 0], [1, 0, 0], [1, 0, 0]]`

**Why?**
The outer multiplication `* R` copied the **reference** to the inner list $R$ times. There is only one inner list in memory, and every row points to it.

---

## The Correct Way: List Comprehensions

To properly initialize a matrix, you must create a new inner list on every iteration. Use a list comprehension.

**✅ Correct Initialization:**
```python
R, C = 3, 3
matrix = [[0] * C for _ in range(R)]
```

Now, modifying one cell works correctly:
```python
matrix[0][0] = 1
print(matrix)
```
**Output:**
`[[1, 0, 0], [0, 0, 0], [0, 0, 0]]`

### Memorize This Pattern
```python
# Create an R x C matrix filled with default_value
matrix = [[default_value] * C for _ in range(R)]
```

---

## Iterating Over a Matrix

### 1. By Index
Use this when you need the coordinates $(r, c)$ for logic.

```python
for r in range(len(matrix)):
    for c in range(len(matrix[0])):
        val = matrix[r][c]
```

### 2. By Value
Use this when you only need to read the values.

```python
for row in matrix:
    for val in row:
        print(val)
```

### 3. Both (Using `enumerate`)
```python
for r, row in enumerate(matrix):
    for c, val in enumerate(row):
        print(f"Cell ({r},{c}) is {val}")
```

---

## Accessing Columns

To extract a specific column from a matrix, use a list comprehension. (Unlike NumPy, standard Python lists don't support `matrix[:, c]`).

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Extract column index 1
col = [row[1] for row in matrix]
print(col) # [2, 5, 8]
```

---

## Time and Space Complexity

- **Time Complexity**: $O(R \times C)$ to initialize the matrix.
- **Space Complexity**: $O(R \times C)$ to store the matrix.

---

## Summary
- **Never** initialize a 2D list using `[[0] * C] * R`.
- **Always** use `[[0] * C for _ in range(R)]`.
- Know how to iterate through a matrix using nested loops and `enumerate`.
