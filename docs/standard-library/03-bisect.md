# `bisect` (Binary Search)

## Introduction

The `bisect` module provides a highly optimized C-implementation of **Binary Search**. 

While you should know how to write a manual binary search loop (many interviewers will ask you to write it from scratch), if the problem merely *uses* binary search as a sub-step, `bisect` is the cleanest way to do it.

---

## `bisect_left` vs `bisect_right`

The primary goal of the module is to find the index where an element should be inserted into a sorted array to maintain its sorted order.

If the element **already exists** in the array, the behavior differs:
- `bisect_left()`: Returns the index of the **first** occurrence (inserts to the left of existing elements).
- `bisect_right()` (or just `bisect()`): Returns the index just after the **last** occurrence (inserts to the right).

```python
import bisect

# A sorted array with duplicates
nums = [1, 3, 3, 3, 5, 7]

# Find where to insert 3
print(bisect.bisect_left(nums, 3))  # 1 (Index of first 3)
print(bisect.bisect_right(nums, 3)) # 4 (Index after last 3)
```

---

## Interview Application: Finding an Element

You can use `bisect_left` to check if an element exists in a sorted array in $O(\log N)$ time.

```python
def binary_search(nums, target):
    index = bisect.bisect_left(nums, target)
    
    # We must check if the index is in bounds 
    # AND if the element at that index is actually our target
    if index < len(nums) and nums[index] == target:
        return index
    return -1
```

---

## Inserting Elements

The module also provides `insort_left()` and `insort_right()`, which find the index *and* insert the element in one step.

```python
nums = [1, 3, 5, 7]

# Finds index 2, then inserts 4
bisect.insort_left(nums, 4)

print(nums) # [1, 3, 4, 5, 7]
```

### 🚨 Common Interview Mistake: `insort` Time Complexity Trap 🚨
Do not use `insort` in a loop assuming it is fast. 

While finding the index is $O(\log N)$, **inserting an element into a list is $O(N)$** because it requires shifting all subsequent elements in memory.

If you use `insort` to build a sorted list of $N$ elements, the total time complexity will be $O(N^2)$. If you need to repeatedly insert elements and maintain sorted order efficiently, you need a balanced Binary Search Tree or a Heap, not a list.

---

## Custom Search Keys

As of Python 3.10, the `bisect` functions support a `key` argument, exactly like `list.sort()`.

```python
intervals = [(1, 5), (3, 7), (8, 10)]

# Find where to insert based on the first element of the tuple
index = bisect.bisect_left(intervals, 4, key=lambda x: x[0])
print(index) # 2
```

*(Note: If you are using an older version of Python, you must manually extract the keys into a separate list before using bisect).*

---

## Time and Space Complexity

- **`bisect_left()` / `bisect_right()`**: $O(\log N)$ time, $O(1)$ space.
- **`insort()`**: $O(N)$ time (due to list insertion overhead), $O(1)$ space.

---

## Summary
- Use `bisect_left(nums, target)` to find the leftmost insertion point (or first occurrence).
- Use `bisect_right(nums, target)` to find the rightmost insertion point.
- Check `nums[index] == target` to confirm the element actually exists.
- **Never** use `insort()` in a loop; list insertions are $O(N)$, resulting in $O(N^2)$ time.
