# Off-By-One Errors

## Introduction

Off-by-one errors (OBOE) are the most common logical bugs in programming. They happen when a loop iterates one time too many, or one time too few.

Python's `range()` function and 0-indexed arrays are designed to minimize these, but they still appear frequently in specific patterns.

---

## Pitfall 1: `range(len(nums))` vs `range(len(nums) - 1)`

When iterating through an array to compare adjacent elements (e.g., `nums[i]` and `nums[i+1]`), you must stop one element early to avoid an `IndexError`.

```python
nums = [1, 2, 3]

# BAD: i will reach 2, and nums[3] throws IndexError
for i in range(len(nums)):
    if nums[i] == nums[i+1]:
        pass

# GOOD: Stops at i = 1
for i in range(len(nums) - 1):
    if nums[i] == nums[i+1]:
        pass
```

---

## Pitfall 2: Including the Stop Index in Slicing/Ranges

Python's `range(start, stop)` and slicing `nums[start:stop]` are **inclusive of the start, but exclusive of the stop**.

If you need to iterate backwards down to 0, using `0` as the stop index will fail because it stops at `1`.

```python
# BAD: Stops at 1
for i in range(5, 0, -1):
    print(i) # Prints 5, 4, 3, 2, 1

# GOOD: Stops at 0
for i in range(5, -1, -1):
    print(i) # Prints 5, 4, 3, 2, 1, 0
```

---

## Pitfall 3: Binary Search Boundaries

Binary Search is notorious for infinite loops and OBOEs. Memorize the exact template to avoid them.

```python
# 1. Use <= to ensure you don't miss the case where left == right
while left <= right:
    mid = left + (right - left) // 2
    
    if nums[mid] == target:
        return mid
    
    # 2. Add/Subtract 1 to shrink the window
    # If you just do left = mid, you will infinite loop when left and right are adjacent
    elif nums[mid] < target:
        left = mid + 1 
    else:
        right = mid - 1
```

---

## Summary
- Compare adjacent elements? Use `range(len(nums) - 1)`.
- Reversing to 0? Use `range(start, -1, -1)`.
- Binary Search? Use `left <= right` and `mid +/- 1`.
