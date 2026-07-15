# Bisect Cheat Sheet

Python's `bisect` module implements binary search on sorted arrays.

```python
import bisect
```

## 1. bisect_left
Finds the insertion point for `x` to maintain sorted order. 
If `x` is already present, it returns the index of the **first** occurrence (the leftmost position).

```python
nums = [10, 20, 20, 20, 30]

idx = bisect.bisect_left(nums, 20)
# Returns 1 (The first '20')

idx = bisect.bisect_left(nums, 25)
# Returns 4 (Insert before '30')
```

## 2. bisect_right (or bisect)
Finds the insertion point for `x` to maintain sorted order.
If `x` is already present, it returns the index **just after** the last occurrence (the rightmost position).

```python
nums = [10, 20, 20, 20, 30]

idx = bisect.bisect_right(nums, 20)
# Returns 4 (Insert after the last '20')
```

## 3. Actually Inserting (insort)
If you want to search *and* insert in one step.
Note: Inserting into a list is $O(N)$ time!

```python
nums = [10, 20, 30]
bisect.insort_left(nums, 25)
# nums is now [10, 20, 25, 30]
```

## Advanced: Using a `key` function (Python 3.10+)
If your list contains objects or tuples, you can provide a `key` function.

```python
pairs = [(1, "a"), (5, "b"), (10, "c")]
idx = bisect.bisect_left(pairs, 5, key=lambda x: x[0])
# Returns 1
```
