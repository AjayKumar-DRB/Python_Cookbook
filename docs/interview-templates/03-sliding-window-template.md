# Sliding Window Template

## The Template

```python
def sliding_window(nums, k):
    left = 0
    current_state = 0 # e.g., sum, count, frequency map
    best_result = 0   # Track max/min
    
    for right in range(len(nums)):
        # 1. ADD: Include nums[right] in current_state
        current_state += nums[right]
        
        # 2. SHRINK: While window violates the constraint
        while current_state > k: # (Replace with actual condition)
            # Remove nums[left] from current_state
            current_state -= nums[left]
            # Move left pointer forward
            left += 1
            
        # 3. UPDATE: Record best result if window is valid
        # e.g., max_length = max(max_length, right - left + 1)
        best_result = max(best_result, right - left + 1)
        
    return best_result
```

## Crucial Reminders
1. **Always expand `right` in a `for` loop.** Do not use two nested `while` loops; it leads to infinite loops if you forget to increment.
2. **Always shrink `left` in a `while` loop.** A single `if` statement is not enough, as a single new element might require dropping multiple old elements.
3. Update the `best_result` **after** the `while` loop finishes. This guarantees the window is valid when you record the score.
