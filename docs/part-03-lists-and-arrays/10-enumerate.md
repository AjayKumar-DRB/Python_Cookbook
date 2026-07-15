# `enumerate()`

## Introduction

In many programming languages, iterating over an array requires a traditional `for` loop with an index variable `i`.

While Python supports `for i in range(len(nums)):`, it is considered un-Pythonic. When you need both the index and the value from a list, always use the built-in `enumerate()` function.

---

## How `enumerate()` Works

`enumerate()` takes an iterable and returns an iterator that yields tuples of `(index, value)`.

```python
fruits = ["apple", "banana", "cherry"]

for index, value in enumerate(fruits):
    print(f"Index {index}: {value}")
```

**Output:**
```
Index 0: apple
Index 1: banana
Index 2: cherry
```

### Specifying a Start Index

You can provide an optional `start` parameter if you want the index to start counting from a number other than `0`.

```python
for count, value in enumerate(fruits, start=1):
    print(f"Item {count}: {value}")
```

---

## When to use `enumerate()`

Use `enumerate()` whenever you need to update an element in place, or when the index itself is part of the problem's logic.

### Example: Modifying a List In-Place

If you need to double every element in a list, you must know the index to overwrite the original value.

```python
nums = [1, 2, 3]

# The Pythonic way
for i, num in enumerate(nums):
    nums[i] = num * 2

print(nums) # [2, 4, 6]
```

### Example: Finding Indices of a Target

In a Two Sum variation, you might need to store the indices of elements in a hash map.

```python
nums = [2, 7, 11, 15]
num_map = {}

for i, num in enumerate(nums):
    num_map[num] = i
```

---

## Common Interview Mistakes

### Mistake: `range(len())` vs `enumerate()`
While `for i in range(len(nums)):` works, it requires you to extract the value manually via `val = nums[i]`. It is slower and less readable. Interviewers familiar with Python expect you to use `enumerate()`.

**Avoid:**
```python
for i in range(len(nums)):
    print(i, nums[i])
```

**Prefer:**
```python
for i, val in enumerate(nums):
    print(i, val)
```

---

## Time and Space Complexity

- **Time Complexity**: $O(N)$ because it iterates through the list exactly once.
- **Space Complexity**: $O(1)$ extra space, as it returns an iterator that yields elements lazily without copying the list.

---

## Summary
- Use `enumerate()` when you need both the index and the value while iterating.
- It returns an iterator of `(index, value)` tuples.
- It is faster, cleaner, and more Pythonic than `range(len())`.
