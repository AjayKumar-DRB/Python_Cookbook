# `itertools` Module

## Introduction

The `itertools` module contains functions for creating iterators for efficient looping. 

In interviews, it is primarily used for **combinatorics** (generating permutations and combinations). If a problem asks you to "generate all possible pairs" or "find all permutations of a string," `itertools` is the fastest way to get the answer.

---

## Combinatorics

### 1. `permutations()`
Returns all possible orderings of an input. Order matters.

```python
import itertools

# Permutations of a string
for p in itertools.permutations("ABC"):
    print("".join(p))
# ABC, ACB, BAC, BCA, CAB, CBA

# Permutations of specific length (e.g., length 2)
list(itertools.permutations("ABC", 2))
# [('A', 'B'), ('A', 'C'), ('B', 'A'), ('B', 'C'), ('C', 'A'), ('C', 'B')]
```
- **Time Complexity**: $O(N!)$ 

### 2. `combinations()`
Returns all possible groupings of an input where order does **not** matter (e.g., AB is the same as BA). You must specify the length.

```python
import itertools

# Combinations of length 2
for c in itertools.combinations("ABC", 2):
    print("".join(c))
# AB, AC, BC
```
- **Time Complexity**: $O(\binom{N}{K})$

### 3. `product()` (Cartesian Product)
Equivalent to nested `for` loops. It returns all possible combinations of drawing one item from each provided iterable.

```python
import itertools

# Equivalent to nested loops
for a, b in itertools.product([1, 2], ['x', 'y']):
    print(a, b)
# 1 x
# 1 y
# 2 x
# 2 y
```
- **Time Complexity**: $O(N \times M)$

---

## Iterators

### `groupby()`
Groups consecutive elements that have the same key. Note: The input **must be sorted** by the grouping key first for this to work properly.

```python
import itertools

data = [("A", 1), ("A", 2), ("B", 3), ("B", 4)]

# Groups by the first element of the tuple
for key, group in itertools.groupby(data, key=lambda x: x[0]):
    print(key, list(group))
# A [('A', 1), ('A', 2)]
# B [('B', 3), ('B', 4)]
```

### `chain()`
Flattens multiple iterables (like a list of lists) into a single iterable without copying them into memory.

```python
import itertools

list1 = [1, 2]
list2 = [3, 4]
list3 = [5, 6]

# Flattens into a single loop
for num in itertools.chain(list1, list2, list3):
    print(num)
```

---

## Interview Constraints

While `itertools` is powerful, **be very careful in interviews**. 

If a problem specifically asks you to "Implement a function to generate all permutations" (like LeetCode 46: Permutations), the interviewer wants you to write the Backtracking algorithm yourself. If you just `return list(itertools.permutations(nums))`, you will fail the interview.

Use `itertools` only when combinatorics is a *sub-step* of a larger problem, not the main goal.

---

## Summary
- Use `permutations()` when order matters ($O(N!)$).
- Use `combinations()` when order does not matter.
- Use `product()` to flatten nested `for` loops.
- Do not use `itertools` if the explicit goal of the problem is to test your Backtracking skills.
