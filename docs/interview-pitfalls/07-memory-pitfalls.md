# Memory Pitfalls

## Introduction

While Time Complexity ($O(N)$) usually dictates if an algorithm passes an interview, Space/Memory Complexity is just as heavily scrutinized.

---

## Pitfall 1: Holding onto massive slices

Python's list slicing (`arr[left:right]`) is incredibly convenient, but it creates a **brand new list** in memory. 

If you are writing a recursive function (like Merge Sort or Binary Search) and you pass slices instead of indices, you will consume massive amounts of memory.

```python
# BAD: O(N) Space per recursive call
def binary_search_bad(nums, target):
    mid = len(nums) // 2
    if nums[mid] == target: return True
    
    if nums[mid] > target:
        # Creates a new list of size N/2!
        return binary_search_bad(nums[:mid], target) 
```

**The Fix:** Always pass the original array by reference, and use `left` and `right` integer pointers to track the current bounds. This requires $O(1)$ space.

```python
# GOOD: O(1) Space per recursive call
def binary_search_good(nums, target, left, right):
    mid = left + (right - left) // 2
    # ...
```

---

## Pitfall 2: `zip()` vs `itertools.izip()` (Python 2 vs 3)

In Python 2, `zip()` created a massive new list in memory. You had to use `itertools.izip()` to get a memory-efficient iterator.

**Good News:** In Python 3, `zip()`, `map()`, `filter()`, and `dict.keys()` all return iterators. They do not allocate memory for the full list until you explicitly wrap them in `list()`. You do not need to worry about this pitfall in modern Python 3.

---

## Pitfall 3: `sys.getsizeof()` vs Interview Space Complexity

If you ever test memory usage locally, do not confuse Python's internal memory overhead with theoretical Big-O Space Complexity.

An empty list in Python might take 56 bytes (`sys.getsizeof([])`), and an integer might take 28 bytes. 
In an interview, you ignore these language-specific constant overheads. 
- Creating an array of $N$ integers is $O(N)$ space.
- Creating 3 variables is $O(1)$ space.
