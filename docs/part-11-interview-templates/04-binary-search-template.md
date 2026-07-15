# Binary Search Template

## The Template

This is the most robust template for Binary Search. It avoids infinite loops and off-by-one errors.

```python
def binary_search(nums, target):
    left = 0
    right = len(nums) - 1
    
    # 1. Use <= so you don't miss the case where left == right
    while left <= right:
        
        # 2. Calculate mid (safe from overflow in other languages)
        mid = left + (right - left) // 2 
        
        if nums[mid] == target:
            return mid # Found it!
            
        elif nums[mid] < target:
            # Target is larger, discard the left half
            # The + 1 prevents infinite loops
            left = mid + 1
            
        else:
            # Target is smaller, discard the right half
            # The - 1 prevents infinite loops
            right = mid - 1
            
    return -1 # Not found
```

## Crucial Reminders
1. **`left <= right`**: If you just use `<`, the loop will terminate early and fail if the array only has 1 element, or if the target is the very last element checked.
2. **`left = mid + 1`** and **`right = mid - 1`**: You already checked `nums[mid]` in the `if` statement, so you know it is not the answer. Exclude it entirely. If you use `left = mid`, the loop will get stuck infinitely when `left` and `right` are adjacent.
3. If the problem asks for the **First Occurrence** of a target, do not `return mid` immediately. Record the index and set `right = mid - 1` to keep searching the left half.
