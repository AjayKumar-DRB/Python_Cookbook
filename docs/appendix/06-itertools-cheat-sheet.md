# Itertools Cheat Sheet

The `itertools` module contains functions for creating iterators for efficient looping.

```python
import itertools
```

## 1. Combinatorics (Combinations & Permutations)

**Combinations**: Order does not matter. `(A, B) == (B, A)`.
```python
items = ['A', 'B', 'C']
list(itertools.combinations(items, 2))
# [('A', 'B'), ('A', 'C'), ('B', 'C')]
```

**Permutations**: Order matters. `(A, B) != (B, A)`.
```python
list(itertools.permutations(items, 2))
# [('A', 'B'), ('A', 'C'), ('B', 'A'), ('B', 'C'), ('C', 'A'), ('C', 'B')]
```

## 2. Cartesian Product
Equivalent to nested `for` loops. Excellent for grid iterations.

```python
# Instead of:
# for r in range(3):
#     for c in range(3):

for r, c in itertools.product(range(3), range(3)):
    print(r, c)
```

## 3. Grouping Items (groupby)
Groups consecutive duplicate elements. **The input must be sorted first!**

```python
items = [1, 1, 1, 2, 2, 3]
for key, group in itertools.groupby(items):
    print(key, list(group))
# 1 [1, 1, 1]
# 2 [2, 2]
# 3 [3]
```

## 4. Pairwise (Python 3.10+)
Iterates over adjacent pairs.
```python
list(itertools.pairwise([1, 2, 3, 4]))
# [(1, 2), (2, 3), (3, 4)]
```

## 5. Accumulate (Prefix Sums)
Returns accumulated sums (or other binary functions).
```python
list(itertools.accumulate([1, 2, 3, 4]))
# [1, 3, 6, 10]
```
