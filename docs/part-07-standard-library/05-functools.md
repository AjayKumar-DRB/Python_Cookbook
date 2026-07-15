# `functools` Module

## Introduction

The `functools` module contains higher-order functions (functions that act on or return other functions). 

For interviews, the most critical feature of this module is the `@lru_cache` decorator, which allows you to implement memoization for Dynamic Programming (DP) in a single line of code.

---

## `@lru_cache` (Memoization Cheat Code)

In Top-Down Dynamic Programming, you write a recursive function and use a dictionary to "cache" (memoize) the results of previous function calls so you don't compute the same subproblem twice.

Instead of manually passing a `memo` dictionary around, you can place the `@lru_cache` decorator above your function. Python will automatically cache the inputs and outputs.

### Example: Fibonacci

**Without `lru_cache` (Manual Memoization):**
```python
def fib(n, memo=None):
    if memo is None:
        memo = {}
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
        
    memo[n] = fib(n-1, memo) + fib(n-2, memo)
    return memo[n]
```

**With `lru_cache` (The Pythonic Way):**
```python
from functools import lru_cache

# maxsize=None means the cache has no size limit
@lru_cache(maxsize=None)
def fib(n):
    if n <= 1:
        return n
    return fib(n-1) + fib(n-2)
```

This reduces the time complexity from $O(2^N)$ to $O(N)$ with literally zero extra logic.

*(Note: In Python 3.9+, you can use `@cache` which is exactly the same as `@lru_cache(maxsize=None)`).*

### Constraints of `@lru_cache`
Because the decorator uses a dictionary under the hood to store the arguments as keys, **all arguments passed to the function must be hashable**.

If your recursive function takes a `list` as an argument, `@lru_cache` will throw a `TypeError`. You must convert the list to a `tuple` before calling the function.

---

## `reduce()`

`reduce()` applies a function of two arguments cumulatively to the items of a sequence, reducing the sequence to a single value.

While list comprehensions and `sum()` are usually preferred, `reduce` is occasionally useful for chained bitwise operations (like finding the cumulative XOR of an array).

```python
from functools import reduce

nums = [1, 2, 3, 4]

# Sum all numbers (equivalent to sum(nums))
total = reduce(lambda a, b: a + b, nums)
print(total) # 10

# Find the cumulative XOR
xor_total = reduce(lambda a, b: a ^ b, nums)
```

---

## `cmp_to_key()`

In older versions of Python (Python 2), you could provide a custom comparison function to `sort()` that returned `-1`, `0`, or `1`. Python 3 removed this in favor of `key` functions.

If a problem requires a highly complex sorting logic (like LeetCode 179: "Largest Number") where you must compare two elements directly to see which comes first, you can use `cmp_to_key` to convert a traditional comparison function into a modern `key` function.

```python
from functools import cmp_to_key

def compare(a, b):
    # If a + b > b + a, a should come first
    if str(a) + str(b) > str(b) + str(a):
        return -1
    return 1

nums = [3, 30, 34, 5, 9]
nums.sort(key=cmp_to_key(compare))

print(nums) # [9, 5, 34, 3, 30]
```

---

## Summary
- Use `@lru_cache(maxsize=None)` or `@cache` to instantly memoize recursive DP functions.
- Ensure all arguments to a cached function are immutable (hashable).
- Use `reduce(lambda a, b: ..., arr)` for cumulative operations across an array.
- Use `cmp_to_key(func)` if you absolutely must write a custom two-variable comparison for sorting.
