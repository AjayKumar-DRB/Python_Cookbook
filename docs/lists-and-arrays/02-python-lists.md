# Python Lists

## Introduction

A list in Python is an ordered, mutable collection of objects. It is the closest equivalent to an "array" in other languages, but with significantly more built-in flexibility.

---

## Creating Lists

You can create lists using square brackets `[]` or the `list()` constructor.

```python
# Empty list
empty1 = []
empty2 = list()

# Initialized list
nums = [1, 2, 3]

# Mixed types (valid, but rare in DSA problems)
mixed = [1, "two", 3.0, [4, 5]]
```

### Pre-allocating Lists

Often in interviews (especially for Dynamic Programming), you need a list of a specific size initialized with a default value.

```python
# Create a list of 10 zeros
dp = [0] * 10
print(dp) # [0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
```
This is an $O(N)$ operation and is highly optimized.

---

## Mutability

Unlike strings, lists are **mutable**. You can modify them in-place without creating a new object.

```python
nums = [1, 2, 3]
nums[0] = 99
print(nums) # [99, 2, 3]
```

### The Shared Reference Trap

Because lists are mutable, assigning one list to another variable does **not** create a copy. Both variables reference the same list in memory.

```python
a = [1, 2, 3]
b = a
b.append(4)

print(a) # [1, 2, 3, 4]
```
If you need an independent copy, use `a.copy()` or `a[:]`.

---

## Lists vs Arrays

In languages like C or Java, an "array" is a contiguous block of memory holding values of the exact same type. The size is fixed at creation.

Python lists are different:
1. **Dynamic Sizing**: They grow and shrink automatically.
2. **Heterogeneous**: They can store elements of different types.
3. **Array of Pointers**: Under the hood, a Python list is an array of *pointers* (references) to the actual objects, not an array of the objects themselves.

If an interviewer asks you to use an "array", they almost always mean a Python `list`. 

*(Note: Python does have an `array` module for C-style arrays of primitives, but it is rarely used in standard algorithmic interviews).*

---

## Summary
- Lists are ordered and mutable.
- `[0] * N` is the idiomatic way to initialize a list of size $N$.
- Assigning `b = a` copies the reference, not the list.
- Python lists are arrays of pointers, meaning they can store mixed data types.
