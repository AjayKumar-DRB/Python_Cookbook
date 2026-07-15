# Indexing and Slicing Lists

## Introduction

Python's list indexing and slicing syntaxes are identical to those used for strings. The key difference is that because lists are mutable, you can use slicing to **modify** or **replace** parts of a list in-place.

---

## Negative Indexing

Python supports negative indexing, which counts from the end of the list.

```python
nums = [10, 20, 30, 40]

print(nums[-1]) # 40 (last element)
print(nums[-2]) # 30 (second to last)
```

This is highly preferred in interviews over `nums[len(nums) - 1]`.

---

## Slicing Syntax

The syntax is `list[start:stop:step]`. It returns a **new list**.

```python
nums = [0, 1, 2, 3, 4, 5]

print(nums[1:4])  # [1, 2, 3]
print(nums[:3])   # [0, 1, 2]
print(nums[3:])   # [3, 4, 5]
```

### Reversing a List

The most Pythonic way to reverse a list is using a step of `-1`.

```python
nums = [1, 2, 3]
rev = nums[::-1]
print(rev) # [3, 2, 1]
```
This takes $O(N)$ time and $O(N)$ space. 

*(Note: If the problem asks for $O(1)$ space, use the in-place method `nums.reverse()` instead).*

---

## Modifying Lists with Slices

Because lists are mutable, you can assign an iterable to a slice. This replaces the targeted slice with the new elements.

```python
nums = [1, 2, 3, 4]

# Replace elements at index 1 and 2
nums[1:3] = [9, 9]
print(nums) # [1, 9, 9, 4]
```

You can even insert or delete elements by assigning iterables of different lengths.

```python
nums = [1, 2, 3]

# Insert without replacing (insert at index 1)
nums[1:1] = [9, 9]
print(nums) # [1, 9, 9, 2, 3]

# Delete a slice (equivalent to del nums[1:3])
nums[1:3] = []
print(nums) # [1, 2, 3]
```

While neat, this is rarely required in standard DSA questions.

---

## Making a Shallow Copy

The most common use of slicing in interviews is creating a quick shallow copy of a list.

```python
nums = [1, 2, 3]
copy_nums = nums[:]
```
This is equivalent to `nums.copy()` and prevents you from accidentally modifying the original list.

---

## Time and Space Complexity

- **Time Complexity**: $O(K)$ where $K$ is the length of the slice.
- **Space Complexity**: $O(K)$ because slicing always allocates a new list in memory.

---

## Summary
- Use `nums[-1]` to get the last element.
- Slicing (`nums[a:b]`) creates a **new list object**.
- Use `nums[::-1]` to create a reversed copy.
- Use `nums[:]` to create a shallow copy.
