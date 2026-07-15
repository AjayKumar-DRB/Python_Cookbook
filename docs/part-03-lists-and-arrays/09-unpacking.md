# Unpacking Iterables

## Introduction

Python allows you to assign elements of a list or tuple to multiple variables in a single, readable line. This is called **unpacking**.

It is widely used in interviews for returning multiple values from a function, swapping variables, or extracting coordinates from a matrix.

---

## Basic Unpacking

If the number of variables on the left matches the number of elements on the right, Python unpacks them sequentially.

```python
point = [10, 20]

# Unpacking the list
x, y = point
print(x) # 10
print(y) # 20
```

### Common Interview Mistake: `ValueError`
If the number of variables does not exactly match the length of the iterable, Python raises a `ValueError`.

```python
# ValueError: too many values to unpack (expected 2)
x, y = [10, 20, 30] 
```

---

## The Swapping Idiom

Because Python evaluates the entire right side before performing any assignments, you can unpack to easily swap variables without a temporary variable.

```python
a = 1
b = 2

a, b = b, a
```
This is the standard, expected way to swap elements in Python.

---

## Advanced Unpacking (The `*` Operator)

If you only care about the first or last few elements of a list, you can use the `*` operator to gather the remaining items into a new list.

```python
nums = [1, 2, 3, 4, 5]

# Get the first element, put the rest in a list
first, *rest = nums
print(first) # 1
print(rest)  # [2, 3, 4, 5]
```

You can put the `*` anywhere.

```python
# First, last, and middle
first, *middle, last = nums
print(first)  # 1
print(middle) # [2, 3, 4]
print(last)   # 5
```

---

## Using `*` in Function Arguments

You can unpack a list directly into function arguments using `*`.

```python
def add(a, b, c):
    return a + b + c

nums = [10, 20, 30]
print(add(*nums)) # 60
```

---

## Time and Space Complexity

- **Time Complexity**: $O(N)$ where $N$ is the number of elements being unpacked.
- **Space Complexity**: $O(1)$ for strict unpacking (assigning references), but $O(K)$ when using `*rest` because a new list of $K$ elements is constructed.

---

## Summary
- Use `a, b = b, a` to swap variables.
- Use `a, *rest = list` to capture arbitrary numbers of elements.
- Unpacking improves code readability and eliminates the need for manual indexing `x = nums[0]; y = nums[1]`.
