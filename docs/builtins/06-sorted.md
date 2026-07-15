# `sorted()`

## Introduction

Python has two ways to sort data:
1. `list.sort()`: An in-place method that modifies a list and returns `None`.
2. `sorted()`: A built-in function that takes any iterable, leaves the original alone, and returns a **new sorted list**.

In interviews, `sorted()` is used when you need to sort strings, tuples, or when you don't want to mutate the original input array.

---

## Basic Usage

```python
nums = [3, 1, 4, 1, 5]

# Returns a new list
ascending = sorted(nums)
print(ascending) # [1, 1, 3, 4, 5]

# The original is untouched
print(nums) # [3, 1, 4, 1, 5]
```

### Sorting Strings
Because strings are immutable, they do not have a `.sort()` method. You must use `sorted()`. Note that `sorted()` always returns a list, so you must join it back into a string.

```python
s = "cba"

# Returns a list of chars
sorted_chars = sorted(s)
print(sorted_chars) # ['a', 'b', 'c']

# Join back to a string
print("".join(sorted(s))) # "abc"
```

---

## The `reverse` Argument

To sort in descending order, use `reverse=True`.

```python
nums = [3, 1, 4, 1, 5]
descending = sorted(nums, reverse=True)
print(descending) # [5, 4, 3, 1, 1]
```

---

## The `key` Argument (Crucial for Interviews)

Just like `min()` and `max()`, `sorted()` accepts a `key` function. This function is called on each element *before* making comparisons.

### Sorting by Length
```python
words = ["apple", "banana", "kiwi", "pear"]

# Sort by length
print(sorted(words, key=len))
# ['kiwi', 'pear', 'apple', 'banana']
```

### Sorting by Multiple Criteria (Tuples)
If you return a tuple from the key function, Python sorts by the first element. If there's a tie, it looks at the second element, and so on.

```python
students = [
    ("Alice", "B", 12),
    ("Bob", "A", 12),
    ("Charlie", "A", 10)
]

# Sort by Grade (ascending), then by Age (descending)
sorted_students = sorted(
    students, 
    key=lambda x: (x[1], -x[2])
)

print(sorted_students)
# [('Charlie', 'A', 10), ('Bob', 'A', 12), ('Alice', 'B', 12)]
```
*(Note: Using `-x[2]` works for integers to reverse the sort order for just that specific field).*

---

## Time and Space Complexity

Python uses **Timsort** (a hybrid of Merge Sort and Insertion Sort).
- **Time Complexity**: $O(N \log N)$ worst/average case. $O(N)$ best case (if already sorted).
- **Space Complexity**: $O(N)$ to create the new list.

---

## Summary
- Use `sorted()` when you need to sort strings or want to keep the original iterable intact.
- Use `reverse=True` for descending order.
- Use `key=lambda x: ...` for custom sorting logic.
- Return a tuple from the `key` function to sort by multiple criteria.
