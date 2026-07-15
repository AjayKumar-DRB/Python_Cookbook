# `sum()`, `min()`, and `max()`

## Introduction

These three aggregation functions are the most commonly used built-ins in algorithmic interviews. Never write manual `for` loops to calculate these values unless the interviewer explicitly asks you to.

---

## `sum()`

Returns the total of all items in an iterable.

```python
nums = [1, 2, 3, 4]
print(sum(nums)) # 10
```

### With a starting value
`sum()` takes an optional second argument: the starting value. This is occasionally useful when you want to sum elements and add them to a baseline offset.

```python
print(sum(nums, 100)) # 110
```
*(Note: Do not use `sum()` to concatenate strings. Use `"".join()` instead).*

---

## `min()` and `max()`

Returns the smallest or largest item in an iterable, or among two or more arguments.

```python
nums = [5, 1, 9, 3]

# From an iterable
print(min(nums)) # 1

# From multiple arguments (useful in DP)
print(max(10, 20)) # 20
```

### Using the `key` argument
Just like `sort()`, you can pass a `key` function to customize how `min()` and `max()` determine the value of an element.

This is highly requested in interviews involving strings or complex objects.

```python
words = ["apple", "banana", "kiwi"]

# Find the longest word
longest = max(words, key=len)
print(longest) # "banana"
```

```python
points = [(1, 5), (3, 2), (8, 10)]

# Find the point with the smallest Y coordinate
lowest_point = min(points, key=lambda p: p[1])
print(lowest_point) # (3, 2)
```

### Providing a `default`
If you call `min()` or `max()` on an empty iterable, Python raises a `ValueError`. To prevent this, you can provide a `default` keyword argument.

```python
empty_list = []

# print(max(empty_list)) # ValueError!

print(max(empty_list, default=0)) # 0
```

---

## Interview Application: Dynamic Programming

In Top-Down DP or recursive Backtracking, `min` and `max` are used constantly to find the optimal path.

```python
# DP state transition example
def min_coins(amount):
    if amount == 0: return 0
    if amount < 0: return math.inf
    
    # Try all coins and take the minimum result
    return 1 + min(min_coins(amount - coin) for coin in coins)
```

---

## Time and Space Complexity

- **Time Complexity**: $O(N)$ for iterables of length $N$.
- **Space Complexity**: $O(1)$.

---

## Summary
- Use `sum()` to add numbers.
- Use `min()` and `max()` to find extremes.
- Use the `key` argument to find extremes based on custom properties (e.g., `key=len`).
- Use `default=0` to prevent `ValueError`s on empty lists.
