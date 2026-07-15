# Bit Manipulation

## Introduction

Bit manipulation involves operating directly on the binary representations (1s and 0s) of numbers using bitwise operators.

These problems are relatively rare but appear frequently in specific companies (like Jane Street or specific hardware teams at FAANG).

---

## Python Bitwise Operators

- **AND (`&`)**: `1 & 1 = 1`, else `0`.
- **OR (`|`)**: `0 | 0 = 0`, else `1`.
- **XOR (`^`)**: `1 ^ 0 = 1`, `1 ^ 1 = 0`. (Returns 1 if bits are different).
- **NOT (`~`)**: Inverts the bits.
- **Left Shift (`<<`)**: Shifts bits left (multiplies by $2^k$).
- **Right Shift (`>>`)**: Shifts bits right (integer division by $2^k$).

---

## The 4 Essential Bit Tricks

If you memorize nothing else, memorize these four operations.

### 1. Check if a Number is Even or Odd
Instead of `n % 2 == 0`, look at the least significant bit.
```python
is_odd = (n & 1) == 1
is_even = (n & 1) == 0
```

### 2. Check if a Number is a Power of 2
A power of 2 (e.g., $16 = 10000_2$) has exactly one `1` bit. Subtracting 1 flips all bits after the `1` ($15 = 01111_2$). Therefore, an AND operation between them results in `0`.
```python
def is_power_of_two(n):
    return n > 0 and (n & (n - 1)) == 0
```

### 3. Clear the Lowest Set Bit
This removes the right-most `1` from the binary representation. Used heavily in Brian Kernighan's algorithm to count set bits.
```python
n = n & (n - 1)
```

### 4. Find the Missing/Single Number (XOR Trick)
XORing a number by itself results in `0` (`A ^ A = 0`). 
XORing a number by `0` results in the number (`A ^ 0 = A`).
Because XOR is commutative, if you XOR an array where every number appears twice except for one, all pairs cancel out, leaving the single number.

```python
# LeetCode 136: Single Number
def single_number(nums):
    result = 0
    for num in nums:
        result ^= num
    return result
```

---

## Bitmasks

A bitmask is an integer used to compactly store a set of booleans. This is extremely useful in Backtracking or DP with state (e.g., Traveling Salesperson Problem), because it turns a list/set into an integer that can be used as a dictionary key or cached via `@lru_cache`.

Let's say we have 5 items, and item 2 and 4 are "selected". 
Binary: `10100` (Read right-to-left: indices 0, 1, 2, 3, 4).
Integer: `20`.

```python
mask = 0

# 1. SET the i-th bit to 1 (Select item i)
i = 2
mask = mask | (1 << i)

# 2. CHECK if the i-th bit is 1 (Is item i selected?)
is_selected = (mask & (1 << i)) != 0

# 3. CLEAR the i-th bit to 0 (Unselect item i)
mask = mask & ~(1 << i)

# 4. TOGGLE the i-th bit (Flip selection)
mask = mask ^ (1 << i)
```

---

## Summary
- **XOR (`^`)** is magic for finding missing/single elements.
- **`n & (n - 1)`** clears the lowest set bit.
- Use **Bitmasks** (`1 << i`) to compactly represent boolean arrays in DP memoization.
