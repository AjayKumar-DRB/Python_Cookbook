# `zip()`

## Introduction

In coding interviews, you will frequently need to iterate over two or more lists simultaneously. 

Instead of managing manual index pointers, Python provides the `zip()` function, which perfectly pairs elements from multiple iterables.

---

## How `zip()` Works

`zip()` takes two or more iterables and groups their elements into tuples based on their index.

```python
names = ["Alice", "Bob", "Charlie"]
scores = [85, 92, 78]

for name, score in zip(names, scores):
    print(f"{name} scored {score}")
```

**Output:**
```
Alice scored 85
Bob scored 92
Charlie scored 78
```

### Handling Unequal Lengths

If the lists are of different lengths, `zip()` automatically stops when the **shortest** iterable is exhausted.

```python
letters = ["a", "b", "c", "d"]
numbers = [1, 2]

# The remaining letters "c" and "d" are ignored
for l, n in zip(letters, numbers):
    print(l, n)
```

*(Note: If you specifically need to iterate until the longest iterable is exhausted, use `itertools.zip_longest()`, though this is rare in interviews).*

---

## When to use `zip()`

Use `zip()` whenever a problem provides multiple parallel arrays or when you need to compare adjacent elements.

### Example: Building a Dictionary
The fastest way to convert two parallel lists into a dictionary mapping keys to values is using `zip()`.

```python
keys = ["name", "age", "city"]
values = ["Alice", 25, "New York"]

person = dict(zip(keys, values))
print(person)
# {'name': 'Alice', 'age': 25, 'city': 'New York'}
```

### Example: Comparing Adjacent Elements
You can zip a list with a sliced version of itself to easily compare adjacent elements.

```python
nums = [1, 3, 7, 8, 10]

# Zip nums (except last) with nums (except first)
for a, b in zip(nums, nums[1:]):
    if b < a:
        print("Not sorted!")
```
This is elegant, though it does create a shallow copy via the slice. For strict $O(1)$ space constraints, use indices instead.

---

## Unzipping

You can "unzip" a list of tuples back into separate lists using the unpacking operator `*` combined with `zip()`.

```python
pairs = [(1, 'a'), (2, 'b'), (3, 'c')]

numbers, letters = zip(*pairs)
print(numbers) # (1, 2, 3)
print(letters) # ('a', 'b', 'c')
```

---

## Time and Space Complexity

- **Time Complexity**: $O(K)$ where $K$ is the length of the shortest iterable.
- **Space Complexity**: $O(1)$ because `zip()` returns a lazy iterator in Python 3. (It does not construct a new list of tuples in memory unless you wrap it in `list()`).

---

## Summary
- Use `zip(list1, list2)` to iterate through multiple lists in parallel.
- `zip()` stops at the shortest list.
- Wrap `zip()` in `dict()` to easily create a mapping from two lists.
- `zip()` is a lazy iterator and uses $O(1)$ extra space.
