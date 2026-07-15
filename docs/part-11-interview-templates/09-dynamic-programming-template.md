# Dynamic Programming Template

## Top-Down (Memoization) Template

This is the standard approach you should use in 95% of interviews. It allows you to write standard recursion and let Python handle the caching.

```python
from functools import cache

def solve_dp(nums):
    
    @cache
    def dp(index, current_state):
        # 1. Base Cases (Out of bounds, reached target, etc.)
        if index >= len(nums):
            return 0
            
        # 2. Recursive Transitions
        # Option A: Take the item
        take = nums[index] + dp(index + 1, current_state_updated)
        
        # Option B: Skip the item
        skip = dp(index + 1, current_state)
        
        # 3. Return Optimal Choice
        return max(take, skip)
        
    # Start the recursion at index 0
    return dp(0, initial_state)
```

## Bottom-Up (Tabulation) Template

Use this if the interviewer explicitly asks to optimize the recursion stack, or if you only need the previous 1-2 states (space optimization).

```python
def solve_dp_bottom_up(n):
    # 1. Initialize DP table
    dp = [0] * (n + 1)
    
    # 2. Base Cases
    dp[0] = 0
    dp[1] = 1
    
    # 3. Build from bottom to top
    for i in range(2, n + 1):
        dp[i] = dp[i-1] + dp[i-2]
        
    return dp[n]
```

## Crucial Reminders
1. **Immutable Arguments**: When using `@cache`, all arguments passed to `dp()` MUST be hashable. If your state requires an array, convert it to a `tuple` before passing it to `dp()`.
2. **Python 3.8 vs 3.9**: `@cache` was added in Python 3.9. If the interview platform uses Python 3.8, you must use `@lru_cache(maxsize=None)`.
