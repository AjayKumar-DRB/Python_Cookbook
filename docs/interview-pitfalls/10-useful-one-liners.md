# Useful One-Liners

## Introduction

These one-liners are not code golf (writing the shortest code possible at the expense of readability). They are established Python idioms that interviewers love to see.

---

## 1. Flatten a 2D Matrix

If you have a matrix and need to process all elements as a flat list, you can use a nested list comprehension.

```python
matrix = [[1, 2], [3, 4]]

# The One-Liner
flat = [val for row in matrix for val in row]

print(flat) # [1, 2, 3, 4]
```

---

## 2. Initialize a 2D Matrix (Safely)

If a DP problem or graph problem requires a 2D grid, you must initialize it correctly.

**DANGER:** `matrix = [[0] * COLS] * ROWS` creates references to the *same* inner list. Modifying `matrix[0][0]` will also modify `matrix[1][0]`.

```python
# The Safe One-Liner
matrix = [[0] * COLS for _ in range(ROWS)]
```

---

## 3. Matrix Transposition

If you need to rotate a grid or process it column-by-column, transpose it.

```python
matrix = [[1, 2], [3, 4]]

# The One-Liner
transposed = list(zip(*matrix))

print(transposed) # [(1, 3), (2, 4)]
```

---

## 4. Conditional Assignment (Ternary Operator)

Instead of a 4-line `if/else` block just to assign a value.

```python
# The One-Liner
val = "Even" if num % 2 == 0 else "Odd"
```

---

## 5. Find First Match or Default

If you want to find the first item in a list that matches a condition, use `next()` with a generator expression.

```python
users = [
    {"id": 1, "status": "offline"},
    {"id": 2, "status": "online"}
]

# Find first online user, or return None if nobody is online
first_online = next((u for u in users if u["status"] == "online"), None)
```

---

## 6. Any / All

To check if a grid is completely valid, or if at least one condition is met, without writing a manual `for` loop with a `return False` inside.

```python
nums = [2, 4, 6, 8]

# Are all numbers even?
is_all_even = all(n % 2 == 0 for n in nums)
```

---

## 7. Merge Two Dictionaries

If you need to combine two state dictionaries (Python 3.9+).

```python
dict1 = {"a": 1}
dict2 = {"b": 2}

# The One-Liner (Python 3.9+)
merged = dict1 | dict2
```
