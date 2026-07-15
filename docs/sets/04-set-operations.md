# Set Operations

## Introduction

Python sets support mathematical set operations like Union, Intersection, and Difference. These operations are highly optimized in C and are extremely useful for solving problems that ask you to compare two collections of data.

---

## Intersection (`&`)

Returns a new set containing only the elements found in **both** sets.

```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}

print(a & b) # {3, 4}
```
### When to use
Use intersection when a problem asks you to find "common elements" between two arrays.

- **Time Complexity**: $O(\min(\text{len}(a), \text{len}(b)))$

---

## Union (`|`)

Returns a new set containing **all unique elements** from both sets.

```python
a = {1, 2, 3}
b = {3, 4, 5}

print(a | b) # {1, 2, 3, 4, 5}
```
### When to use
Use union when combining multiple lists of results and you need to ensure no duplicates exist in the final output.

- **Time Complexity**: $O(\text{len}(a) + \text{len}(b))$

---

## Difference (`-`)

Returns a new set containing elements that are in the first set, but **not** in the second set.

```python
a = {1, 2, 3, 4}
b = {3, 4}

print(a - b) # {1, 2}
```
### When to use
Use difference when you need to filter a collection against a list of "invalid" or "seen" items.

- **Time Complexity**: $O(\text{len}(a))$

---

## Symmetric Difference (`^`)

Returns a new set containing elements that are in **either** set, but **not both**.

```python
a = {1, 2, 3}
b = {2, 3, 4}

print(a ^ b) # {1, 4}
```
### When to use
Use symmetric difference when a problem asks you to find elements that appear exactly once across two arrays.

- **Time Complexity**: $O(\text{len}(a) + \text{len}(b))$

---

## In-Place Updates

All of the above operators create a **new set**. If you want to modify an existing set in place to save memory, use the assignment versions:

- `&=` (intersection_update)
- `|=` (update)
- `-=` (difference_update)
- `^=` (symmetric_difference_update)

```python
a = {1, 2, 3}
b = {3, 4, 5}

a &= b # Modifies 'a' directly
print(a) # {3}
```

---

## Summary
- Use `&` (Intersection) for common elements.
- Use `|` (Union) to combine uniquely.
- Use `-` (Difference) to remove specific elements.
- Use `^` (Symmetric Difference) for exclusively unique elements.
- Use the `x=` versions for in-place modifications to save memory.
