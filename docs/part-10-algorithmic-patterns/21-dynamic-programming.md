# Dynamic Programming (DP)

## Introduction

Dynamic Programming is a method for solving complex problems by breaking them down into simpler subproblems. It is an optimization over plain recursion.

Whenever a recursive algorithm computes the same subproblems repeatedly, you can optimize it using DP.

---

## How to Recognize It

Use DP when the problem asks for:
- The **Maximum / Minimum / Longest / Shortest** path or cost.
- The **Total Number of Ways** to reach a goal.
- Evaluating if it's **Possible** to reach a goal (True/False).
- And the problem contains "overlapping subproblems" (e.g., Fibonnaci, where calculating Fib(4) requires calculating Fib(3) and Fib(2)).

---

## Top-Down DP (Memoization)

Top-Down DP starts at the final goal and recursively breaks the problem down. 

To prevent redundant calculations, you store the results of function calls in a dictionary (the "memo"). In Python, you can do this effortlessly using the `@cache` or `@lru_cache` decorator from `functools`.

### Example: Climbing Stairs
How many distinct ways can you climb to the top of an $N$-step staircase, if you can take 1 or 2 steps at a time?

```python
from functools import cache

def climb_stairs(n):
    
    @cache
    def dp(step):
        # Base Cases
        if step == n:
            return 1 # Reached the top! (1 way)
        if step > n:
            return 0 # Overshot the top! (0 ways)
            
        # Recursive Step: Ways to reach top from (step+1) + ways from (step+2)
        return dp(step + 1) + dp(step + 2)
        
    return dp(0)
```
*(Note: Because of `@cache`, `dp(step)` is computed exactly once for each step. Time complexity drops from $O(2^N)$ to $O(N)$).*

---

## Bottom-Up DP (Tabulation)

Bottom-Up DP avoids recursion entirely. It starts at the base cases and uses a `for` loop to build an array (the "DP table") up to the final goal.

```python
def climb_stairs_bottom_up(n):
    if n <= 2:
        return n
        
    dp = [0] * (n + 1)
    dp[1] = 1
    dp[2] = 2
    
    for i in range(3, n + 1):
        dp[i] = dp[i - 1] + dp[i - 2]
        
    return dp[n]
```

### Space Optimization
In many bottom-up DP solutions (like Fibonnaci/Stairs), the current state `dp[i]` only depends on the previous two states `dp[i-1]` and `dp[i-2]`. 

You do not need an entire $O(N)$ array! You only need two variables. This drops the space complexity to $O(1)$.

```python
def climb_stairs_optimized(n):
    if n <= 2:
        return n
        
    one_step_before = 2
    two_steps_before = 1
    
    for i in range(3, n + 1):
        current = one_step_before + two_steps_before
        
        # Shift the variables for the next iteration
        two_steps_before = one_step_before
        one_step_before = current
        
    return one_step_before
```

---

## Which one should I use in an interview?

If you struggle with DP, **always use Top-Down (Memoization) with `@cache`**. 
It is easier to conceptualize (you just write the brute-force recursion and add a decorator), and it only computes states that are strictly necessary.

Interviewer follows ups:
- *Can you optimize the space?* -> Convert it to Bottom-Up, and if possible, use state-reduction (variables instead of arrays).

---

## Summary
- Use DP for Max/Min/Ways problems with overlapping subproblems.
- **Top-Down**: Recursion + `@cache`. Easy to write, $O(N)$ time, $O(N)$ space.
- **Bottom-Up**: Iteration + Array. No recursion limit risks.
- **Optimized**: Iteration + Variables. $O(1)$ space.
