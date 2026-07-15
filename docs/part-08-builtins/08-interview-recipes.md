# Built-ins Interview Recipes

## Introduction

Python's built-in functions allow you to replace massive chunks of boilerplate code with single, elegant lines. Here are the most common patterns expected in interviews.

---

## Recipe 1: Matrix Transposition with `zip`

When a problem asks you to rotate a matrix or process columns instead of rows (e.g., Valid Sudoku), you need to transpose it.

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# *matrix unpacks the rows, zip pairs the elements by column
transposed = [list(col) for col in zip(*matrix)]

# transposed is now:
# [
#   [1, 4, 7], 
#   [2, 5, 8], 
#   [3, 6, 9]
# ]
```

---

## Recipe 2: Validating Grids with `all()`

If you need to verify that all rows or columns meet a condition, use `all()` with a generator expression.

```python
def is_valid_sudoku_row(row):
    # Ignore dots (empty cells) and ensure no duplicates
    seen = set()
    return all(
        val == '.' or (val not in seen and not seen.add(val)) 
        for val in row
    )
```
*(Note: `not seen.add(val)` is a neat trick since `add()` returns `None`, so `not None` is `True`, allowing the `all()` check to continue).*

---

## Recipe 3: Multi-Criteria Sorting

When sorting objects by primary and secondary conditions, pass a `lambda` to `sorted` that returns a tuple.

```python
files = [
    {"name": "a.txt", "size": 100},
    {"name": "b.txt", "size": 200},
    {"name": "c.txt", "size": 100}
]

# Sort by size (ascending), then by name (descending)
# Note: String descending sorting requires 'reverse=True' usually, 
# but for mixed fields, you can just sort twice!

# Python's sort is stable, so sort by secondary condition first:
files.sort(key=lambda x: x["name"], reverse=True)
# Then sort by primary condition:
files.sort(key=lambda x: x["size"])
```

---

## Recipe 4: Mapping Input Data

For HackerRank or competitive programming style inputs.

```python
# If input is "4 5 6"
line = "4 5 6"

# Convert to integers cleanly
a, b, c = map(int, line.split())
```

---

## Summary
- **Transpose**: `list(zip(*matrix))`
- **Validate**: `return all(condition for x in items)`
- **Stable Sort**: When sorting by multiple fields where you need descending strings, sort multiple times taking advantage of Timsort's stability.
- **Parse Inputs**: `map(int, string.split())`
