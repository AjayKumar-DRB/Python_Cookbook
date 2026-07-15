# List Comprehensions

## Introduction

List comprehensions provide a concise, readable, and highly optimized way to construct lists. They replace the pattern of creating an empty list and calling `append()` inside a `for` loop.

In a Python interview, list comprehensions prove that you are comfortable with the language's idioms.

---

## The Syntax

The basic syntax is:
`[expression for item in iterable]`

```python
nums = [1, 2, 3, 4]

# Traditional loop
squares = []
for n in nums:
    squares.append(n * n)

# List Comprehension (Pythonic)
squares_comp = [n * n for n in nums]
```

---

## Adding Conditions (Filtering)

You can filter elements by adding an `if` condition at the end.

`[expression for item in iterable if condition]`

```python
nums = [1, 2, 3, 4, 5, 6]

# Keep only even numbers
evens = [n for n in nums if n % 2 == 0]
print(evens) # [2, 4, 6]
```

---

## If-Else Expressions (Mapping)

If you need to change the output depending on a condition, the `if-else` block moves to the **front**, before the `for`.

`[true_expr if condition else false_expr for item in iterable]`

```python
nums = [1, -2, 3, -4]

# Replace negatives with 0
clamped = [n if n > 0 else 0 for n in nums]
print(clamped) # [1, 0, 3, 0]
```

---

## Nested Comprehensions

You can use nested list comprehensions to flatten a 2D matrix or build a new one. The loops are read from left to right.

```python
matrix = [
    [1, 2],
    [3, 4]
]

# Flatten the matrix
flat = [val for row in matrix for val in row]
print(flat) # [1, 2, 3, 4]
```

*(Note: Don't nest comprehensions more than two levels deep, as they become unreadable. Use regular loops instead).*

---

## Performance Considerations

List comprehensions are faster than manual `for` loops with `.append()`.

Why? Because the list comprehension logic is executed directly in C, bypassing the overhead of looking up the `.append()` method on every iteration.

However, the time complexity remains the same.

- **Time Complexity**: $O(N)$
- **Space Complexity**: $O(N)$ (it allocates a completely new list)

---

## Generator Expressions vs Comprehensions

If you replace the square brackets `[]` with parentheses `()`, you create a **generator expression**.

```python
# List comprehension (evaluates immediately, takes O(N) memory)
squares_list = [n * n for n in range(1000000)]

# Generator expression (evaluates lazily, takes O(1) memory)
squares_gen = (n * n for n in range(1000000))
```

Use a generator expression when passing the result directly to functions like `sum()`, `max()`, or `all()` to save space.

```python
total = sum(n * n for n in range(1000000)) # O(1) space
```

---

## Summary
- Use `[expr for item in list]` instead of standard loops with `.append()`.
- Put `if` at the end for filtering.
- Put `if ... else ...` at the front for conditional mapping.
- Use `(expr for item in list)` for $O(1)$ space lazy evaluation.
