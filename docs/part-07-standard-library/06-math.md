# `math` Module Essentials

## Introduction

The `math` module provides essential mathematical constants and operations. While it contains dozens of functions, you only need to memorize a few core constants and methods for Data Structures and Algorithms (DSA) interviews.

---

## `math.inf` (Infinity)

In problems involving finding a minimum or maximum value, you often need to initialize a tracker variable. 

Do not use arbitrary numbers like `9999999` or `-1` (unless constraints specifically allow it). The Pythonic way is to use `math.inf` and `-math.inf`.

```python
import math

def find_min(nums):
    # Initialize to positive infinity
    min_val = math.inf 
    
    for num in nums:
        if num < min_val:
            min_val = num
            
    return min_val
```

An alternative is using `float('inf')`, which does not require importing the `math` module, though `math.inf` is often preferred for readability.

---

## `math.gcd()`

The Greatest Common Divisor (GCD) is frequently required in math-heavy interview questions (e.g., simplifying fractions, finding periods). 

Do not write your own Euclidean algorithm loop. Use `math.gcd()`.

```python
import math

print(math.gcd(10, 15)) # 5
```

---

## `math.ceil()` and `math.floor()`

When performing division, you often need to round the result.

- `math.floor(x)`: Rounds down to the nearest integer.
- `math.ceil(x)`: Rounds up to the nearest integer.

```python
import math

# Normal division
val = 5 / 2 # 2.5

print(math.floor(val)) # 2
print(math.ceil(val))  # 3
```

### The Integer Division Trick (Without `math`)
You can avoid importing `math` by using Python's integer division `//`.
- **Floor Division**: `5 // 2` is `2`.
- **Ceiling Division Trick**: `-( -5 // 2 )` is `3`. (Because `-5 // 2` evaluates to `-3`, and negating it gives `3`).

While the ceiling trick is extremely fast, `math.ceil()` is much more readable in an interview.

---

## `math.log()` and `math.log2()`

If a problem asks you to check if a number is a power of 2, or requires calculating tree depths mathematically, use the logarithmic functions.

```python
import math

# Check if N is a power of 2 (assuming N > 0)
def is_power_of_two(n):
    # log2(n) should be an integer
    return math.log2(n).is_integer()
```
*(Note: The bitwise approach `n & (n - 1) == 0` is the optimal way to check powers of 2, but `math.log2` works well for general cases).*

---

## Time and Space Complexity

- **`math.gcd(a, b)`**: $O(\log(\min(a, b)))$ time.
- All other mentioned functions (`inf`, `floor`, `ceil`, `log`): $O(1)$ time.

---

## Summary
- Use `math.inf` and `-math.inf` to initialize min/max trackers.
- Use `math.gcd(a, b)` instead of writing a manual Euclidean algorithm.
- Use `math.floor(x)` and `math.ceil(x)` for explicit rounding.
