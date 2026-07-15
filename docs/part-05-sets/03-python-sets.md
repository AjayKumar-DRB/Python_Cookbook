# Python Sets

## Introduction

A Python `set` is an unordered, mutable collection of unique elements. 

---

## Creating Sets

You can create a set using curly braces `{}` or the `set()` constructor.

```python
# Create a set with elements
nums = {1, 2, 3}

# Create from an iterable (removes duplicates automatically)
chars = set("hello")
print(chars) # {'h', 'e', 'l', 'o'}
```

### The Empty Set Trap
You **cannot** create an empty set using `{}`. That creates an empty dictionary. You must use `set()`.

```python
empty_dict = {}
print(type(empty_dict)) # <class 'dict'>

empty_set = set()
print(type(empty_set)) # <class 'set'>
```

---

## Modifying Sets

Because sets are unordered, they do not have `append()` (which implies adding to the end) or `insert()` (which requires an index).

### Adding Elements
Use `add()` to insert a single element.

```python
nums = {1, 2}
nums.add(3)
nums.add(2) # Adding a duplicate does nothing
print(nums) # {1, 2, 3}
```
- **Time Complexity**: $O(1)$

### Removing Elements
There are two ways to remove elements:

1. `remove(x)`: Removes the element, but raises a `KeyError` if it doesn't exist.
2. `discard(x)`: Removes the element if it exists; does nothing if it doesn't.

```python
nums = {1, 2, 3}
nums.discard(99) # Safe, does nothing

# nums.remove(99) # Raises KeyError
```
- **Time Complexity**: $O(1)$

If you need to remove an arbitrary element, use `pop()`. It returns a random element from the set (useful in some graph algorithms).

---

## Membership Testing (`in`)

The primary reason to use a set in an interview is for fast membership testing using the `in` operator.

```python
nums = {1, 2, 3, 4, 5}

if 3 in nums:
    print("Found!")
```
- **Time Complexity**: $O(1)$

---

## Unordered Nature

Sets do not maintain insertion order (unlike modern Python dictionaries). 
You cannot access elements by index (`nums[0]` will raise a `TypeError`), and iterating over a set yields elements in a seemingly random order based on their hash values.

```python
chars = set("banana")
for char in chars:
    print(char) # Order is not guaranteed
```

---

## Time and Space Complexity

- **Time Complexity**: $O(1)$ for add, remove, and `in`. $O(N)$ to iterate.
- **Space Complexity**: $O(N)$ to store $N$ elements.

---

## Summary
- Use `set()` to create an empty set, not `{}`.
- Use `add()`, `remove()`, and `discard()` to modify sets.
- Use `in` for $O(1)$ membership testing.
- Sets are unordered and do not support indexing.
