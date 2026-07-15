# Two Pointers Templates

## Template 1: Converging (Opposite Ends)
Used for sorted arrays, palindromes, and Container With Most Water.

```python
def two_pointers_converging(nums):
    left = 0
    right = len(nums) - 1
    
    while left < right: # STRICTLY less than to avoid comparing an element to itself
        current_val = nums[left] + nums[right]
        
        if current_val == target:
            return True
        elif current_val < target:
            # Need a larger value
            left += 1
        else:
            # Need a smaller value
            right -= 1
            
    return False
```

## Template 2: Fast & Slow (Same Direction)
Used for Linked List cycle detection, finding the middle, and in-place array modifications (removing duplicates).

```python
def fast_slow_pointers(head):
    slow = head
    fast = head
    
    # Must check both fast and fast.next to avoid AttributeError
    while fast and fast.next:
        slow = slow.next          # Move 1 step
        fast = fast.next.next     # Move 2 steps
        
        if slow == fast:
            return True # Cycle detected
            
    # If loop finishes, fast reached the end
    return False 
```

## Crucial Reminders
1. **Converging**: Always use `while left < right:`. Do not use `<=`, or you will process the middle element twice or compare it to itself.
2. **Fast/Slow**: Always guard the loop with `while fast and fast.next:`. If you only check `fast`, `fast.next.next` will crash when `fast.next` is `None`.
