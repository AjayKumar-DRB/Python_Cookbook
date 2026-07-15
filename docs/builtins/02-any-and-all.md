# `any()` and `all()`

## Introduction

The `any()` and `all()` functions take an iterable and evaluate the truthiness of its elements. They are incredibly useful for writing concise conditional checks in interviews.

---

## `any()`

Returns `True` if **at least one** element in the iterable evaluates to `True`. If the iterable is empty, it returns `False`.

```python
bools = [False, False, True, False]
print(any(bools)) # True
```

### Short-Circuit Evaluation
`any()` stops evaluating as soon as it finds the first `True` value.

```python
def check_positive(n):
    print(f"Checking {n}")
    return n > 0

nums = [-1, -2, 5, -4]
# Stops printing after "Checking 5"
result = any(check_positive(x) for x in nums) 
```

---

## `all()`

Returns `True` if **every** element in the iterable evaluates to `True`. If the iterable is empty, it returns `True`.

```python
bools = [True, True, True]
print(all(bools)) # True
```

### Short-Circuit Evaluation
`all()` stops evaluating as soon as it finds the first `False` value.

```python
nums = [1, 2, -5, 4]
# Stops evaluating when it hits -5
result = all(x > 0 for x in nums) 
print(result) # False
```

---

## Combining with Generator Expressions

The true power of `any()` and `all()` in interviews comes from combining them with generator expressions. This allows you to replace multi-line `for` loops with a single, readable line of code.

### Example: Checking a Valid Sudoku Row
Instead of:
```python
def is_valid(row):
    for val in row:
        if val < 1 or val > 9:
            return False
    return True
```

Write:
```python
def is_valid(row):
    return all(1 <= val <= 9 for val in row)
```

### Example: Finding an Overlap
Instead of:
```python
def has_overlap(list1, list2):
    set2 = set(list2)
    for x in list1:
        if x in set2:
            return True
    return False
```

Write:
```python
def has_overlap(list1, list2):
    set2 = set(list2)
    return any(x in set2 for x in list1)
```

---

## Time and Space Complexity

- **Time Complexity**: $O(N)$ in the worst case (it must check every element). $O(1)$ in the best case due to short-circuiting.
- **Space Complexity**: $O(1)$ when used with a generator expression. (Warning: Using a list comprehension `[x > 0 for x in nums]` forces $O(N)$ space before `any()` even starts. Always use generators `(...)`).

---

## Summary
- Use `any()` to check if *at least one* condition is met.
- Use `all()` to check if *all* conditions are met.
- Both functions short-circuit to save time.
- Always use them with generator expressions `(condition for item in iterable)` to save space.
