# Sorting Lists

## Introduction

Many algorithms—especially greedy algorithms, interval problems, and two-pointer setups—require you to sort the input data first.

Python provides highly optimized built-in sorting mechanisms. You should virtually never write your own sorting algorithm (like QuickSort or MergeSort) in an interview unless specifically asked to.

---

## `sort()` vs `sorted()`

There are two ways to sort a list in Python:

### 1. `list.sort()` (In-Place)
Modifies the original list directly and returns `None`. Use this when you want to save space and don't need the original order.

```python
nums = [3, 1, 4, 1, 5]
nums.sort()
print(nums) # [1, 1, 3, 4, 5]
```
- **Time Complexity**: $O(N \log N)$
- **Space Complexity**: $O(N)$ auxiliary space (Timsort requires additional memory, it is not strictly $O(1)$).

### 2. `sorted(list)` (Creates a Copy)
Returns a brand-new sorted list, leaving the original unchanged. Use this when the input array must not be mutated.

```python
nums = [3, 1, 4, 1, 5]
new_nums = sorted(nums)
```
- **Time Complexity**: $O(N \log N)$
- **Space Complexity**: $O(N)$ to store the new list.

---

## Sorting in Reverse

Both methods accept a `reverse=True` parameter to sort in descending order.

```python
nums = [3, 1, 4]
nums.sort(reverse=True)
print(nums) # [4, 3, 1]
```

---

## Custom Sorting with `key`

The most powerful feature of Python's sorting is the `key` parameter. It accepts a function that computes a sorting key for each element.

### Sorting by Length
```python
words = ["apple", "banana", "kiwi", "pear"]
words.sort(key=len)
print(words) # ['kiwi', 'pear', 'apple', 'banana']
```

### Sorting with Lambda Functions
For custom logic, use an anonymous `lambda` function.

**Example: Sort a list of tuples by the second element**
```python
intervals = [(1, 3), (2, 6), (8, 10)]

# Sort by the end time (index 1)
intervals.sort(key=lambda x: x[1])
```

### Sorting by Multiple Criteria
Return a tuple from the lambda function to sort by primary, then secondary, criteria.

**Example: Sort by length, then alphabetically**
```python
words = ["apple", "banana", "kiwi", "pear", "plum"]

# Sort by length first (len(x)), then alphabetically (x)
words.sort(key=lambda x: (len(x), x))
print(words) 
# ['kiwi', 'pear', 'plum', 'apple', 'banana']
```

---

## Timsort (Under the Hood)

Python's built-in sort uses an algorithm called **Timsort** (a hybrid of Merge Sort and Insertion Sort). 

Interviewers may ask about its properties:
- **Time Complexity**: $O(N \log N)$ worst/average case, $O(N)$ best case (if already sorted).
- **Space Complexity**: $O(N)$ worst-case auxiliary space.
- **Stability**: Yes. Timsort is a **stable** sort, meaning elements with equal keys remain in their original relative order.

---

## Summary
- Use `sort()` for in-place sorting and `sorted()` to get a new list.
- Use `reverse=True` for descending order.
- Use `key=lambda x: ...` for custom sorting logic, returning a tuple for multiple criteria.
- Python uses **Timsort** ($O(N \log N)$ time, $O(N)$ space, stable).
