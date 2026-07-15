# `list.sort()` vs `sorted()`

## Introduction

Python offers two distinct ways to sort iterables. Choosing the right one in an interview demonstrates your understanding of memory management and mutability.

---

## 1. `list.sort()` (In-Place)

The `.sort()` method belongs strictly to the `list` class. It sorts the list **in place** and returns `None`.

```python
nums = [3, 1, 4, 1, 5]

# Sorts the original list, returns None
result = nums.sort()

print(nums)   # [1, 1, 3, 4, 5]
print(result) # None
```

### When to use `list.sort()`
Use `.sort()` when you are given a list, you don't need to preserve the original order, and you want to save memory.
- **Space Complexity**: $O(N)$ (Timsort still requires some extra memory, though it sorts the container in place).

### Common Interview Trap
Because `.sort()` returns `None`, you cannot chain it or use it in an assignment.

```python
# TypeError: 'NoneType' object is not iterable
# for num in nums.sort():
#     print(num)

# Incorrect assignment
# sorted_nums = nums.sort() 
```

---

## 2. `sorted()` (Out-of-Place)

The `sorted()` function is a built-in function that takes *any* iterable (lists, strings, tuples, dictionaries) and returns a **new sorted list**.

```python
nums = [3, 1, 4, 1, 5]

# Creates a brand new list
new_nums = sorted(nums)

print(nums)     # [3, 1, 4, 1, 5] (Unchanged)
print(new_nums) # [1, 1, 3, 4, 5]
```

### Sorting Strings and Tuples
Because strings and tuples are immutable, they do not have a `.sort()` method. You **must** use `sorted()`.

```python
s = "cba"
# Returns a list, must join back to string
sorted_str = "".join(sorted(s)) 
```

### When to use `sorted()`
Use `sorted()` when you need to sort an immutable iterable, or when the problem requires you to preserve the original array.
- **Space Complexity**: $O(N)$ to create the new list, plus $O(N)$ for the Timsort algorithm.

---

## Summary
- Use `list.sort()` to mutate a list in place and save memory. Remember it returns `None`.
- Use `sorted(iterable)` for strings, tuples, or when you need a new list. It always returns a list.
