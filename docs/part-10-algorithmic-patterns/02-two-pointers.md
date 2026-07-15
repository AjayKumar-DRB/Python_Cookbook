# Two Pointers

## Introduction

The Two Pointers pattern involves iterating through an array using two references (pointers) that move toward each other, or move in the same direction at different speeds.

It is highly memory-efficient, usually operating entirely in-place ($O(1)$ space).

---

## How to Recognize It

Use Two Pointers when:
- The input array is **sorted**.
- You need to find pairs that sum to a target.
- You need to reverse an array or string in-place.
- You are comparing elements at opposite ends of an array (e.g., checking for palindromes).

---

## Pattern 1: Opposite Ends (Converging)

Used when the array is sorted, or when you are comparing endpoints (like Palindromes or Container With Most Water).

```python
def two_sum_sorted(nums, target):
    left = 0
    right = len(nums) - 1
    
    while left < right:
        current_sum = nums[left] + nums[right]
        
        if current_sum == target:
            return [left, right]
        elif current_sum < target:
            # We need a larger sum, move left pointer right
            left += 1
        else:
            # We need a smaller sum, move right pointer left
            right -= 1
            
    return []
```

---

## Pattern 2: Same Direction (Fast/Slow)

Used when modifying an array in place, like removing duplicates or moving zeroes to the end.

```python
def move_zeroes(nums):
    # 'slow' keeps track of where the next non-zero should go
    slow = 0
    
    # 'fast' scans the array
    for fast in range(len(nums)):
        if nums[fast] != 0:
            # Swap them
            nums[slow], nums[fast] = nums[fast], nums[slow]
            slow += 1
```

*(Note: Fast/Slow pointers are heavily used in Linked Lists to detect cycles. We cover this specifically in the Fast and Slow Pointers / LinkedList section).*

---

## Time and Space Complexity

- **Time Complexity**: $O(N)$. The pointers scan the array at most once. (If you have to sort the array first, the total time becomes $O(N \log N)$).
- **Space Complexity**: $O(1)$. You only need two integer variables for the pointers.

---

## Summary
- If the array is sorted and you need pairs, put pointers at the `left` and `right` ends and converge.
- If you need to mutate an array in-place by filtering elements, use a `slow` pointer to track the insertion index, and a `fast` pointer to scan.
- Complexity is usually $O(N)$ time and $O(1)$ space.
